---
title: "Database Indexes"
date:  2026-01-25
categories: ["Lazy Bird Project"]
tags: []
---

## Introduction

Imagine you are looking for a recipe in a recipe book of 1000 pages. You don't know exactly which page the recipe that you are looking for is it. What do you have to do? You have to run over every single of the 1000 pages of the book, trying to find that one of your interest. Maybe your recipe is located in the last page of the book and you still don't know about it. So, only after desperating fliping all the book pages, you finally get your recipe and now you can go to the kitchen to prepare that beatiful Chocolate Cake that you are craving for. Now, let's suppose that instead of having to flip all the 1000 pagens, in the very first page of the book there is a page of indexes. Two columns. One for the name of the recipes, and one for the page number that the recipe is located. Now, instead of running over 1000 pages, you just have to read a single page until you find your desired recipe. 

This is exactly how Databases Indexes works and what is it made for. 

## Database Indexes

Databases Indexes are nothing but a way to improve the performance of getting a value in a database. Whenever you create a new table in a database, you should be able to define which column (or columns) can be used as an index for all the values that will be stored in this table. 

### Why does it matter?

Just like the introduction history about the chocolate cake recipe, databases indexes are a way to make database read faster. When we are handling just a small amount of data, the benefits from it are not so obvious (think about a recipe book with only 10 pages). However, as soon as the database size is growing, they are more than necessary, they are required. You can't spend most of your processing time flipping pages and pages of data in the database. 

### Scenario

Let's imagine that you need to create a new table for Brazilian citizens. We know that every brazilian has a name, a surname and a CPF, which is an ID, formed by 11 numbers, provided by the government. We also no that names and surnames are not uniques among all the people. It's quite common having two people with the same name and surname, not only in Brazil. The CPF number on other side is unique for each person, thus a perfect choice for our index. That way, when you create your table, you must to set CPF as an index for this table. For example:

```sql
CREATE TABLE IF NOT EXISTS brazilian_citizen (
      id SERIAL PRIMARY KEY,
      cpf VARCHAR(12) NOT NULL UNIQUE,
      name VARCHAR(255) NOT NULL,
      surname VARCHAR(255) NOT NULL,
  );

CREATE INDEX idx_brazilian_citizen_cpf ON brazilian_citizen(cpf);
```

__

Importante to mention that in SQL, if you set a column as a primary key, it will be set automatically as an index. 

With a table created like this, anytime you query something filtering by the cpf value, the query executor will look first to the index page in order to get the correct value instead of running over all ther table records to get the information of a single citizen. 

### Composed Indexes

There are some cases that is convenient to create indexes composed by more than one column. Let's supposed that we don't have an unique identifier like CPF but we still have names and surnames. Query by the name only is still not efficient, since it's an information that can have too many duplications throughout the database. Only surname, for the same reason, is not a good way to efficiently filter citizens. However, the combination of name and surname can generate results fast enough. So, you can create a composed index formed by name and surname, like this:

```sql
CREATE TABLE IF NOT EXISTS brazilian_citizen (
      id SERIAL PRIMARY KEY,
      name VARCHAR(255) NOT NULL,
      surname VARCHAR(255) NOT NULL,
  );

CREATE INDEX idx_brazilian_citizen_name_surname ON brazilian_citizen(name, surname);
```

It works exactly the same as the single column index. 

## Problems

Let's return to our recipe book. Imagine now that you are the writer and since you care a lot about your readers, you make sure to create an index for your book. But it's still being written and anytime you add a new recipe (or remove one), you need to spend some time updating the index page. That's what is called the write overhead on database indexes. You should be aware of that because depending on the circunstances, you may introduce some latency on your operations due to this overhead. That's why you need to choose your indexes wisely, making sure that the benefits of having them are not shadowed by the write overhead.  

## Conclusion

The database indexes are one of the most easy, basic and straightforward way to improve the performance of a database. In any production code, is mandatory to provide the most adequate indexes for each table. Forgetting to set them up or setting them up wrongly, can lead you to a database with a really poor performance. 

## Further Reading

If you want to learn more about it, you should visit these links:

-  
-  
-  
