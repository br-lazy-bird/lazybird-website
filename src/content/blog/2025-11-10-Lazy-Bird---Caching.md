---
title: "Caching"
date:  2025-11-10
categories: ["Lazy Bird Project"]
tags: []
---

## Introduction

You worked really hard last year and can finally have some vacation time. You decide to visit your parents' hometown. You will visit your uncles, aunts, grandparents, and all sorts of relatives who haven't seen you and your parents for a long time. Whenever you meet a new relative, they ask you: "How are your parents?" So, to provide the most accurate response, you take your phone, call them, and say: "Hey, Uncle José is asking how you are. How are you?" They answer you, and you then answer your relative with: "They've just said they're alright. Thank you." But this is getting ridiculous. You're spending most of your time making calls to your parents, who are also craving some peace during their vacation. So, you decide to call them early every morning and keep that information for the day. Every single relative who asks will receive the same information, which will only be updated the next morning.

This is exactly how caching works. You get a piece of information, keep it with you for a specific amount of time that you find appropriate, and give it to whoever asks. After this specific amount of time expires, you then update the information.

## Caching

Caching is a brilliant solution and a powerful tool to make systems run more efficiently. It relies on the speed of access of the system's internal memory. Getting a value from memory is much faster than getting it from API calls, database queries, or disk. So, the idea is to keep in memory chunks of data that are most commonly accessed and update them accordingly. This "accordingly" means something different for each kind of data we are working on.

### Why Does It Matter?

Caching matters because memory access is fast and cheap. Implementing it in your system means reducing a lot of I/O operations and latency, and it's a key concept for efficient and scalable systems.

### Scenario

Whenever you have data that is stable enough to keep in memory, that's an indication of a caching opportunity. Let's say we need to get addresses for people. We know that usually, under normal circumstances, people don't move from their address every day, or month, or maybe even every year. Most people tend to live at the same address for years. So, if we have a system that displays people's addresses and we have a specific person who is really popular, we can cache their address. Whenever a new request for that popular person's address comes in, we can just look into memory instead of calling an API or querying the database.

## Problems

Caching has some interesting problems to solve and strategies to implement. One of the most important is understanding how often your data changes in order to determine how often your cache should be updated. In some cases, staleness is not a big deal.

Let's think about a weather app. There are very few situations where a difference of a few degrees Celsius would matter to people. If you see that it's 20°C but it's actually 21°C or 19°C, that's not a big deal. And we know that temperature doesn't change much within a period of one hour. So, we can definitely hit the Weather API just once every hour and cache the information for all the requests made during this period.

In other cases, the fresher the better, and caching will harm your system. Real-time systems, for example, can handle only a little or maybe zero caching. Applications that monitor traffic jams like Waze must show real-time information to users. So, it doesn't make sense to cache information about crowded or empty streets, because it can change suddenly and make the user really angry.

So, to determine when and how to implement caching, you really need to understand not only your data but also the expected user experience and how you will handle stale data. To make sure that your cache provides good data, you need to implement some invalidation strategy. In this post, we won't go into too much detail, but we basically have these options:

- As soon as you hit a value that has been stale for longer than expected (Time-To-Live or TTL), fetch it from the API and refresh the cache.
- Create an async service that keeps looking for stale values and refreshes them.
- Invalidate cache when some specific event happens.
- Etc.

## Conclusion

Caching is an indispensable concept and tool in software development and should be used whenever possible. We should have a deep knowledge of the nature of the data and the user experience that our system wants to provide so we can determine the best strategy for implementing caching and the right balance between stale and fresh data, without harming the performance and latency of the system.

## Further Reading

If you want to learn more about it, you should visit these links:

- **Python Caching Libraries:** https://github.com/long2ice/fastapi-cache - FastAPI-native caching with support for Redis and Memcached backends
- **Caching Best Practices:** https://aws.amazon.com/caching/ - Comprehensive guide to caching patterns and when to use them
- **Redis Documentation:** https://redis.io/docs/ - Industry-standard distributed caching solution for production systems