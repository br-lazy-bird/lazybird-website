---
title: "Parallel API Calls"
date:  2025-11-01
categories: ["Lazy Bird Project"]
tags: []
---

## Introduction

Imagine that you have a small retail food store that connects local producers to your customers. You have two employees whose job is to go to the local producers to get the products that you will sell in your store. Among all the producers, there are two who live far away from each other: one provides you cheese and another one provides wine. You could ask a single employee to go get both products. The employee would go to the cheese producer on the north side, taking about 10 minutes to get there, and then another 20 minutes to go to the wine producer on the south side, taking 30 minutes for the whole trip. But you have two employees, and if you ask them to get the goods for you, each one going to a different producer, the amount of time spent to have all the products will be 20 minutes instead of 30. A fair amount of time saved that can be the key for you to remain the most efficient retail store in the region.

This scenario describes the difference between sequential and parallel operations. You can see this pattern in lots of different domains, but it is a really important concept in software development.

## Parallelism

Parallel calls are calls that are triggered at the same time, with each one performing a separate operation. They can be to external and internal APIs, but also to databases or any external resource. The most important concept for creating parallel calls is the fact that the calls don't depend on each other. If they do depend on each other, you must call them sequentially.

Sequential calls, on the other hand, are calls that need to be executed in a specific order. Using the little story from the introduction, let's imagine that the wine producer is an old-fashioned producer who doesn't like money but accepts cheese as payment. So, to get your wine order, you first need to buy some cheese. In that case, it doesn't make sense to send both of your employees, each one to a different producer, to get your products. You can send just one, and they will first get the cheese and only then be able to get the wine.

### Why Does It Matter?

When writing APIs, latency matters. So if you are able to parallelize your calls, that's a really quick win. With that, you will be able to reduce your response time and provide a smoother user experience.

### Scenario

Let's say we are working on a social network and we need to show the user profile page that will contain personal and professional data. Each set of information is located in a different API, and both of them require only the user_id, which is available since login.

```python
personal_data = await client.get(f"{PERSONAL_SERVICE_URL}/{user_id}")
professional_data = await client.get(f"{PROFESSIONAL_SERVICE_URL}/{user_id}")
```

As you can see, we have two calls to make, and since both of them require only the user_id, we don't need to wait for one to complete before making the other call. We can just call them in parallel, like this:

```python
personal_response, professional_response = await asyncio.gather(
    client.get(f"{PERSONAL_SERVICE_URL}/{user_id}"),
    client.get(f"{PROFESSIONAL_SERVICE_URL}/{user_id}")
)
```

That way, the time spent to complete both calls will only be the time spent to complete the slowest one.

## Problems

First, we need to be completely aware of the requirements of each API call to make sure that they are actually parallelizable. But more important than this, you need to have a deep understanding of how your parallel library works because you need to provide the correct approach for handling errors or timeouts. Handling parallel problems is not only a concern of the software engineering layer but also the product layer. Let's get back to the personal and professional profile example. If for some reason showing only the personal data is enough to load a page, you must use a library that makes it possible to get the result of the Personal API call even if the Professional API returns an error or times out. However, if your UX requires both pieces of information, you must write your code to abort the execution if one of the parallel calls fails, and obviously implement the proper handling for this scenario with retries, exponential backoff, and eventually showing a server error.

## Conclusion

Parallelism is a powerful tool for making API calls efficiently and providing a good user experience. But in order to get the most out of it, it's important to have a complete understanding of the APIs' requirements and behaviors to make sure that two or more calls can actually be parallelized.

## Further Reading

If you want to learn more about it, you should visit these links:

- **Python asyncio Documentation:** https://docs.python.org/3/library/asyncio.html - Official Python documentation covering coroutines, tasks, and asyncio.gather()
- **Concurrency vs Parallelism Explained:** https://testdriven.io/blog/python-concurrency-parallelism/ - Understanding the differences between concurrency and parallelism, and when to use each for I/O-bound vs CPU-bound tasks
