---
title: "Parallel API calls"
date:  2026-01-25
categories: ["Lazy Bird Project"]
tags: []
---


## Introduction

Imagine that you have a small retail food store that connects local producers to your customers. You have two employees that their job is go to the local producers to get the products that you will sell in your store. Among all the producers there are two, that lives far away from each other: one that provides you cheese and another one for wine. You can ask for a single employee to go get both products. The employee would go to the chesse producer, in the north side, taking about 10 minutes to get there and then more 20 minutes to go to the wine producer, in the south side, tooking 30 minutes for the whole trip. But you have two employees and if you ask them to get the goods for you, each one to one distinct producer the amount of time spent to have all the products will be 20 minutes, instead of 30. A faire amount of time that can be the key for you to remain as the most eficcient retailer store of the region.

This scenario describes the diference between sequencial and parallel operations and you can see this pattern and lots of different domains, but it is a really important concept during software development.


## Parallelism 

Parallel calls are those calls that are triggered at the same time and each one performs a separate call. It can be to external and internal APIs, but also database or any external resource. The most important concept to create parallel calls is the fact that the calls don't depend on each other. If that is the case, you must to call them sequentially. 

Sequential calls on the other hand are calls that needs to be executed in a determined order. Using the little story of the introduction, let's imagine that the wine producer is an old-fashioned producer that don't like money but accepts cheese as payment. So, to get your wine order you first need to buy some cheese. In that way, it does not make sense to send both of your employees, each one for each producer, to get your products. You can send just one and this one will first get the cheese and only then they will be able to get the wine. 

### Why Does It Matter?

When writing APIs, latency matters. So if you are allowed to parallelize your calls, that's a really quick win. With that, you will be able to reduce your response time and to provide a smoother user experience.

### Scenario

Let's say we are working on a social network and we need to show the user profile page that will contain: personal and professional data, each one set of information located in a different API and both of them requiring only the user_id, which is available since the login. 

```python
personal_data = await client.get(f"{PERSONAL_SERVICE_URL}/{user_id}")
professional_data = await client.get(f"{PROFESSIONAL_SERVICE_URL}/{user_id}")
```

As you can see, we have two calls to make and, since both of them requires only the user_id, we don't need to wait one to complete to make the other call. We can just call them in parallel, like this:

```python
personal_response, professional_response = await asyncio.gather(
    client.get(f"{PERSONAL_SERVICE_URL}/{user_id}"),
    client.get(f"{PROFESSIONAL_SERVICE_URL}/{user_id}")
)
```

That way, the time spent to complete both calls will be only the time spend to complete the slowest one. 

## Problems

First, we need to be completely aware of the requirements of each API call to make sure that they are really parallelisable. But more important than this, you need to have a deep understanding of how your parallel library works because you need to provide the correct approach for eventual errors or timeouts. Handling with parallel problems is not a concern of the software engineering layer but also the product one. Let's get back to the personal and professional profile example. If for some reason showing only the personal data is enough to load a page, you must use a library that will make it possible to get the result of the Personal API call even if the Professional API returns error or gets timeout. However, if your UX requires both of information, you must write your code in order to abort the execution if one of the parallel calls fails and, obviously, implementing the proper handling for this scenario with retries, exponential backoff and eventually showing server error. 

## Conclusion

Parallelism is a powerfull tool to make eficiently API calls and providing a good user experience. But in order to get most of it, it's important the total comprehension of the APIs requirements and behaviours to make sure that two or more calls can be in fact parallelized or not.

## Further Reading

If you want to learn more about it, you should visit these links:

-  
-  
-