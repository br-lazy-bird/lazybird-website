---
title: "Database Locking"
date:  2026-01-19
categories: ["Lazy Bird Project"]
tags: []
---

## Introduction

Before talking about software development, let’s shift our domain a little. Imagine a small farm with a single piece of land used by two farmers to grow tomatoes for sale. Two customers arrive at the same time. Each customer is assisted by one farmer and asks whether tomatoes are available.

Customer A asks Farmer A if there are tomatoes. Customer B, on the other hand, asks Farmer B if there are tomatoes available and, if so, wants to buy all of them.

Farmer A goes to the field, sees that there are tomatoes, and returns to Customer A with a positive answer. Customer A then says they want to buy all the tomatoes. However, in the meantime, Farmer B also went to the field, saw that tomatoes were available, and took all of them for Customer B.

When Farmer A returns to the field to collect the tomatoes for Customer A, there are no tomatoes left.

This is a classic problem of concurrent access to a shared resource. It does not happen only in software. But since this is a software engineering blog, let’s return to our domain.

## Race Conditions

A race condition is a scenario in which a system's behavior depends on the sequence or timing of other uncontrollable events, leading to unexpected or inconsistent results [^1]. The scenario of checking a resource and modifying it later is known as the *check-then-act* pattern, also referred to as TOCTOU (time-of-check to time-of-use).

In databases, this problem manifests when more than one service or process needs to read the same database row and update it later. Depending on the circumstances, the database state may change in the time window between the read operation and a subsequent write operation within a specific transaction.

Fortunately, these problems are well known, and we already have ways to prevent them. In general, there are two main approaches: pessimistic locking and optimistic locking.

## Pessimistic Locking 

Pessimistic locking is based on the assumption that race conditions are likely to happen, so the system must be designed to prevent them upfront. This approach is typically implemented using row-levels locks.

When a transaction reads a database row, it also acquires a lock on that row, preventing other transactions from modifying it until the lock is released. The row is unlocked only after the transaction finishes its work related to that data. Meanwhile, any other transaction that needs to access the same row must wait. 

This strategy prioritizes correctness by enforcing mutual exclusion, at the cost of reduced concurrency.

## Optimistic Locking

Optimistic locking assumes that race conditions will occur only in specific situations. For this reason, locking happens only at update time. 

All transactions are free to read the row concurrently, but when an update is required, the transaction must specify the version of the row it is updating. If another transaction has modified the row in the meantime, the version will no longer match and the update will fail. When this happens, the transaction must repeat its work, ensuring that the database remains in a valid state. 

This approach favors concurrency and performance in the common case, accepting the cost of retries when conflicts occur. 

## Choosing Between Them

Choosing between pessimistic and optimistic locking is fundamentally a trade-off between **latency**, **throughput** and the **cost of conflicts**.

Latency refers to how long a single operation takes to complete. Throughput refers to how many operations the system can complete over a period of time. Locking strategies affect both.

Pessimistic locking tends to increase latency, since transactions may need to wait for locks to be released. It also limits throughput under contention, because fewer transactions can proceed in parallel. However, it provides strong guarantees of correctness and avoids retries.

Optimistic locking allows a higher degree of parallelism. Reads are fast, and writes are fast when conflicts are rare. This typically results in lower latency and higher throughput in low-contention systems. When contention increases, however, failed updates and retries can increase latency and reduce effective throughput.

To choose between these approaches, some key questions to consider are:

- Does the system perform more reads or writes?
- Low or High Contention?
- How expensive are conflicts when they occur?
- How sensitive is the system to increased latency?

For example, a heavy-read system such as an e-commerce catalog typically has low contention and can benefit from optimistic locking. In contrast, a heavy write system with high contention, such as an e-commerce checkout where many customers attempt to buy the same product simultaneously, often requires pessimistic locking. 

Systems that are critical in terms of data consistency, such as financial systems, have little to no tolerance for race conditions. In these cases, sacrificing some throughput and latency in favor of correctness is usually the right choice. On the other hand, for systems like wiki platforms, conflicts are generally less harmful, making optimistic locking a reasonable option.

### Rule of Thumb to choose

| Factor               | Pessimistic                               | Optimistic                                   |
  |----------------------|-------------------------------------------|----------------------------------------------|
  | Contention           | High (many users, same resource)          | Low (rare conflicts)                         |
  | Conflict cost        | High (overselling is unacceptable)        | Low (retry is acceptable)                    |
  | Transaction duration | Short (quick lock-and-release)            | Long (user editing for minutes)              |
  | Read/Write ratio     | Write-heavy                               | Read-heavy                                   |
  | Failure mode         | Block and wait                            | Fail and retry                               |
  | Example use case     | Flash sales, seat booking, bank transfers | Profile updates, CMS editing, config changes |

  Quick decision:
  - "Can I afford to retry?" → Optimistic
  - "Can I afford to block?" → Pessimistic

## Common Pitfalls

Once a locking strategy is chosen, it is important to consider what can go wrong after it is implemented.

### Deadlock

With pessimistic locking, one possible issue is a deadlock. This occurs when two or more transactions wait for each other to release locks, creating a circular dependency that prevents progress.

One effective way to prevent it is to enforce a **consistent global ordering of locks**. This means that all transactions must acquire locks in the same predefined order. For example, if a system operates on multiple related entities, such users and orders, every transaction must always acquire the lock on the **user** entity before acquiring the lock on the **order** entity. By ensuring all transactions request locks in the same sequence, circular wait conditions are eliminated, making deadlocks impossible by design.

Another complementary mechanism is the use of lock timeouts. If a transaction holds a lock for longer than expected, the system can abort or roll back the transaction, releasing the lock and allowing others to proceed. To apply timeouts safely, it is essential to clearly define transaction boundaries, so that locks are not released too early or held for too long. 

 ### Retries Storm

 With optimistic locking, a common issue is a retry storm. When a transaction fails to update a row due to a version conflict, it may retry the operation. If many transactions retry at the same time without proper control, this can overload the database and degrade system performance. 

 To mitigat this problem, it is important to limit the number of retries and introduce random delays between attempts. This reduces contention and prevents the system from amplifying the very issue it is trying to solve.

## Conclusion

Race conditions are a serious issue that can negatively affect both systems and users. However since this is a long-standing and well-understood problem, there are established strategies to mitigate it. 

Understanding the trade-offs between pessimistic and optimistic locking in terms of latency, throughput and conflict cost, enables engineers to make better decisions and build systems that are both safe and efficient.

## Further Reading

For readers interested in going deeper into concurrency, locking strategies, and their trade-offs, the following resources provide detailed and authoritative discussions:

Designing Data-Intensive Applications – Chapter 7: Transactions [^2]
Martin Kleppmann explores race conditions, isolation levels, pessimistic and optimistic locking, and the fundamental trade-offs between consistency, latency, and throughput in modern data systems. 


PostgreSQL Documentation – Explicit Locking [^3]
An in-depth explanation of how database-level locks work in practice, including row-level locks, lock modes, and how deadlocks are detected and resolved.

---

[^1]: [https://en.wikipedia.org/wiki/Race_condition](https://en.wikipedia.org/wiki/Race_condition)
[^2]: [https://dataintensive.net/](https://dataintensive.net/)
[^3]: [https://www.postgresql.org/docs/current/explicit-locking.html](https://www.postgresql.org/docs/current/explicit-locking.html)
