---
title: "Understanding Race Conditions"
date: 2026-01-15
description: "Learn how race conditions occur in multi-threaded environments and how to prevent them."
tags: ["concurrency", "database", "locking"]
---

Race conditions occur when multiple processes or threads access shared resources simultaneously, and the final outcome depends on the timing of their execution.

## What is a Race Condition?

A race condition happens when:

1. Multiple processes access a shared resource
2. At least one process modifies the resource
3. The outcome depends on the order of execution

## The Check-Then-Act Pattern

One of the most common causes of race conditions is the "check-then-act" pattern, also known as TOCTOU (Time-of-Check to Time-of-Use):

```python
# Dangerous pattern
if product.quantity > 0:
    # Another process might change quantity here!
    create_order(product)
    product.quantity -= 1
```

## How to Prevent Race Conditions

### Pessimistic Locking

Lock the resource before reading:

```python
product = db.query(Product).with_for_update().first()
if product.quantity > 0:
    create_order(product)
    product.quantity -= 1
```

### Optimistic Locking

Detect conflicts at commit time using version numbers:

```sql
UPDATE products
SET quantity = quantity - 1, version = version + 1
WHERE id = ? AND version = ?
```

## Learn by Doing

Try the [Flash Sales](/systems) broken system to experience and fix a race condition yourself!
