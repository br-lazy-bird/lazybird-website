---
title: "Database Indexes"
date:  2025-10-01
categories: ["Lazy Bird Project"]
tags: []
---

## Introduction

Imagine you are looking for a recipe in a cookbook with 1,000 pages. You don't know exactly which page contains the recipe you're looking for. What do you have to do? You have to go through every single one of the 1,000 pages, trying to find the one you're interested in. Maybe your recipe is on the last page of the book, and you won't know until you get there. So, only after desperately flipping through all the pages, you finally find your recipe and can go to the kitchen to prepare that beautiful Chocolate Cake you've been craving. Now, let's suppose that instead of flipping through all 1,000 pages, the book has an index page right at the beginning. Two columns: one for the recipe names, and one for the page numbers where each recipe is located. Now, instead of going through 1,000 pages, you just need to scan a single page to find your desired recipe.

This is exactly how database indexes work and what they are made for.

## Database Indexes

Database indexes are simply a way to improve the performance of retrieving values from a database. When you create a new table in a database, you can define which column (or columns) should be used as an index for the values stored in that table.

### Why Does It Matter?

Just like the cookbook story in the introduction, database indexes are a way to make database reads faster. When we're handling just a small amount of data, the benefits aren't so obvious (think about a cookbook with only 10 pages). However, as the database grows, indexes become more than necessary, they become essential. You can't spend most of your processing time scanning through pages and pages of data in the database.

### Scenario

Let's imagine that you need to create a new table for Brazilian citizens. Every Brazilian has a name, a surname, and a CPF, an ID formed by 11 digits, provided by the government. We also know that names and surnames are not unique among all people. It's quite common to have two people with the same name and surname, not only in Brazil but everywhere. The CPF number, on the other hand, is unique for each person, making it a perfect choice for our index. That way, when you create your table, you should set CPF as an index. For example:

```sql
CREATE TABLE IF NOT EXISTS brazilian_citizen (
      id SERIAL PRIMARY KEY,
      cpf VARCHAR(12) NOT NULL UNIQUE,
      name VARCHAR(255) NOT NULL,
      surname VARCHAR(255) NOT NULL
  );

CREATE INDEX idx_brazilian_citizen_cpf ON brazilian_citizen(cpf);
```

Important to mention: **in SQL, if you set a column as a primary key, it will automatically be set as an index**.

With a table created like this, whenever you query something filtering by the CPF value, the query executor will look at the index first to find the correct value, instead of scanning all the table records to get the information of a single citizen.

### Composite Indexes

There are some cases where it's convenient to create indexes composed of more than one column. Let's suppose that we don't have a unique identifier like CPF, but we still have names and surnames. Querying by name alone is still not efficient, since names can have many duplicates throughout the database. Surname alone, for the same reason, is not a good way to efficiently filter citizens. However, the combination of name and surname can produce results fast enough. So, you can create a composite index using name and surname, like this:

```sql
CREATE TABLE IF NOT EXISTS brazilian_citizen (
      id SERIAL PRIMARY KEY,
      name VARCHAR(255) NOT NULL,
      surname VARCHAR(255) NOT NULL
  );

CREATE INDEX idx_brazilian_citizen_name_surname ON brazilian_citizen(name, surname);
```

It works exactly the same as a single-column index.

## Problems

Let's return to our cookbook. Imagine now that you are the author, and since you care a lot about your readers, you make sure to create an index for your book. But the book is still being written, and every time you add a new recipe (or remove one), you need to spend time updating the index page. This is called write overhead in database indexes. You should be aware of this because, depending on the circumstances, you may introduce latency in your operations due to this overhead. That's why you need to choose your indexes wisely, making sure that the benefits of having them are not overshadowed by the write overhead.

## Conclusion

Database indexes are one of the easiest, most basic, and straightforward ways to improve database performance. In any production code, it's mandatory to provide the most appropriate indexes for each table. Forgetting to set them up, or setting them up incorrectly, can lead to a database with very poor performance.

## Further Reading

If you want to learn more about it, you should visit these links:

-  PostgreSQL Official Documentation - Indexes: https://www.postgresql.org/docs/current/indexes.html
-  Use The Index, Luke (e-book): https://use-the-index-luke.com/
-  Secret To Optimizing SQL Queries - Understand The SQL Execution Order: https://www.youtube.com/watch?v=BHwzDmr6d7s