---
title: "N+1 Queries Problem"
date:  2026-01-25
categories: ["Lazy Bird Project"]
tags: []
---


## Introduction

A situation where you first get superficial information and only them you get more in depth ones. 

You are a school director in a school with 3 rooms with 10 children each. You know that a government assistent will visit the school to get a rough idea of how satisfied the children are with the food at school. Knowing that the assistent will not talk to all the children, you just go to the 3 rooms and ask for the list of names of the children. As soon as the assistent arrives and ask the information about an specific child, you go together to the respective room and talk to the specific child. So, in the case that the assistent want to talk to 3 children of each room, you will need to go 3 times to each room. 3 visits to get the list of names, plus 3 times for each room is equal to 12 visits. 

However, the result is not good and they realized that a lot of children has food allergies or restrictions and now they want to know this information from each single child. Now, it's not efficient to go to the room to talk to every child. They would need to go 10 times to each room for it, which would result in 33 visits. Instead, the director goes to every room just once, collect the all the information of every child in that room and then moves to the next room. When the assisten arrives and ask for the information, you already get everything they wants with the just 3 initial visits. 

The first scenario describes the lazy loading approach. Knowing that you don't need all the information at once, you just get the "pointers" to the information (the list of children in our case) and as soon as you need more details, you fetch it. However, as you can see, lazy loading can result in a high number of "visits". Think about the case where there are 100 rooms with 30 children each. The number of visits would be massive.

This lazy loading scenario causing a lot of "visits" is called N+1 Queries problem in databases and that's what we will discuss in this post.

## N+1 Queries

Just like the school story described in the introduction session, N+1 queries is an issue that manifests when our ORM library implements lazy loading when fetching data. For small datasets or depending on the circunstances, lazy loading can be very helpful, providing fast results for the first layer of the query. However, for larger datasets it becomes the bottleneck due to high amount the queries executed. 

### Code Example

Let's see a code snippet showcasing this issue:

**Example in SQLAlchemy (Python):**
```python
# This looks like one query...
orders = session.query(Orders).all()

# But this triggers N queries (one per order):
for order in orders:
    print(order.customer.name)  # Query 1, Query 2, Query 3...
    print(len(order.items))     # Query 501, Query 502, Query 503...
```

As we can see, the SQLAlchemy implements the lazy loading but anytime we need to fetch the details of an order, we have more queries for it, making the whole operation slow and expensive. 

It's not a issue by itself, but if we are in a situation where we need all the data at once, we definitely should change the implementation.


### The Fix

To fix this behaviour, we use an approach called **Eager Loading** which is basically leveraging SQL JOINS or IN to reduce the numbers of query:

1. JOIN-Based: it is best for one-to-one or many-to-one relationships, it is translated in a single query but it can have duplicated rows in the result. Using SQLALchemy, it can be implemented like this:

```python
# Orders and Customers is an one-to-one relationship.
# Each order has one and only one customer.
orders  = sesson.query(Orders).options(joinedload(Orders.customer))
```

The SQL translation for it is:

**SQL Example:**
```sql
SELECT orders.*, customers.*
FROM orders
LEFT JOIN customers ON orders.customer_id = customers.id;
```

That's why single query and eventual duplications (JOIN).

2. IN-Based or Separated Query Loading: best for one-to-many relationships, it is translated in more than one query but still way less than N+1 and it doesn't have duplications in its results.

```python
# Orders and Items is an one-to-many relationship.
# Each order can have one or more items.
orders  = sesson.query(Orders).options(selectinload(Orders.items))
```

The SQL translation for this one is:

```sql
-- Query 1: Fetch main records
SELECT * FROM orders;

-- Query 2: Fetch all records related to order items in one batch
SELECT * FROM order_items
WHERE order_id IN (1, 2, 3, ..., 500);
```

That's why it is translated in more than one query, but it doesn't generate duplication on results.

In our code example, we will need both customers and items informations, so we can do the following:

```python
# Orders and Customers is an one-to-one relationship.
# Each order has one and only one customer.
orders  = sesson.query(Orders)
            .options(joinedload(Orders.customer))
            .options(selectinload(Orders.items))
```

## Conclusion

The N+1 problem is not a bug but a side effect of a default approach of ORMs libraries. The code is running as it should be, but depending on the scenario, the result and performance is degraded. We have well-known approaches to work around it and it depends on the type of relation between the data. Having a deep knowledge of the dataset, the relationship among the tables and the user experience that we want to provide is fundamental key to implement an efficient code.

## Further Reading

If you want to learn more about it, you should visit these links:

-  
-  
-