---
title: "N+1 Queries Problem"
date:  2025-12-20
categories: ["Lazy Bird Project"]
tags: []
---

## Introduction

You are a school principal at a school with 3 classrooms, each with 10 children. You know that a government assistant will visit the school to get a rough idea of how satisfied the children are with the school food. Knowing that the assistant won't talk to all the children, you just go to the 3 classrooms and get the list of names. As soon as the assistant arrives and asks for information about a specific child, you go to the respective classroom, bring them to your room, and let the assistant talk to that child. So, if the assistant wants to talk to 3 children from each classroom, you will need to go to each classroom 3 times. 3 visits to get the lists of names, plus 3 visits to each classroom equals 12 visits.

However, the results aren't good. They realize that many children have food allergies or restrictions, and now they want this information from every single child. Now, it's not efficient to go to the classroom to talk to each child individually. You would need to go 10 times to each classroom, which would result in 30 visits. Instead, you go to every classroom just once, collects all the information from every child in that room, and then moves to the next one. When the assistant arrives and asks for the information, you already have everything they need from just the 3 initial visits.

The first scenario describes the lazy loading approach. Knowing that you don't need all the information at once, you just get the "pointers" to the information (the list of children in our case), and as soon as you need more details, you fetch them. However, as you can see, lazy loading can result in a high number of "visits". Think about the case where there are 100 classrooms with 30 children each. The number of visits would be massive.

This lazy loading scenario causing a lot of "visits" is called the N+1 Queries problem in databases, and that's what we will discuss in this post.

## N+1 Queries

Just like the school story described in the introduction, the N+1 queries problem is an issue that manifests when our ORM library implements lazy loading when fetching data. For small datasets, or depending on the circumstances, lazy loading can be very helpful, providing fast results for the first layer of the query. However, for larger datasets, it becomes a bottleneck due to the high number of queries executed.

### Code Example

Let's see a code snippet showcasing this issue:

**Python (SQLAlchemy):**
```python
# This looks like one query...
orders = session.query(Orders).all()

# But this triggers N queries (one per order):
for order in orders:
    print(order.customer.name)  # Query 1, Query 2, Query 3...
    print(len(order.items))     # Query 501, Query 502, Query 503...
```

As we can see, SQLAlchemy implements lazy loading, but every time we need to fetch the details of an order, we have more queries for it, making the whole operation slow and expensive.

It's not an issue by itself, but if we are in a situation where we need all the data at once, we should definitely change the implementation.

### The Fix

To fix this behavior, we use an approach called **Eager Loading**, which basically leverages SQL JOINs or IN clauses to reduce the number of queries:

1. **JOIN-Based**: This is best for one-to-one or many-to-one relationships. It translates to a single query but can have duplicated rows in the result. Using SQLAlchemy, it can be implemented like this:

```python
# Orders and Customers is a one-to-one relationship.
# Each order has one and only one customer.
orders = session.query(Orders).options(joinedload(Orders.customer))
```

The SQL translation for it is:

**SQL Example:**
```sql
SELECT orders.*, customers.*
FROM orders
LEFT JOIN customers ON orders.customer_id = customers.id;
```

That's why we get a single query and possible duplications (due to the JOIN).

2. **IN-Based or Separate Query Loading**: This is best for one-to-many relationships. It translates to more than one query but still far fewer than N+1, and it doesn't have duplications in its results.

```python
# Orders and Items is a one-to-many relationship.
# Each order can have one or more items.
orders = session.query(Orders).options(selectinload(Orders.items))
```

The SQL translation for this one is:

```sql
-- Query 1: Fetch main records
SELECT * FROM orders;

-- Query 2: Fetch all records related to order items in one batch
SELECT * FROM order_items
WHERE order_id IN (1, 2, 3, ..., 500);
```

That's why it translates to more than one query, but it doesn't generate duplicate results.

In our code example, we need both customer and item information, so we can do the following:

```python
# The proper approach for each relationship
orders = session.query(Orders)
            .options(joinedload(Orders.customer))
            .options(selectinload(Orders.items))
```

## Conclusion

The N+1 problem is not a bug but a side effect of a default approach in ORM libraries. The code is running as it should, but depending on the scenario, the result and performance are degraded. We have well-known approaches to work around it, and the choice depends on the type of relationship between the data. Having a deep knowledge of the dataset, the relationships among the tables, and the user experience we want to provide is fundamental to implementing efficient code.

## Further Reading

If you want to learn more about it, you should visit these links:

- **SQLAlchemy specifics:** [Relationship Loading Techniques](https://docs.sqlalchemy.org/en/20/orm/queryguide/relationships.html)
- **Other ORMs:** Django ([select_related](https://docs.djangoproject.com/en/stable/ref/models/querysets/#select-related)), Hibernate ([Fetching](https://docs.jboss.org/hibernate/orm/current/userguide/html_single/Hibernate_User_Guide.html#fetching)), ActiveRecord ([Eager Loading](https://guides.rubyonrails.org/active_record_querying.html#eager-loading-associations))