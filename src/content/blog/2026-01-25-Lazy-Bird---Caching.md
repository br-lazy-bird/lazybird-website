---
title: "Caching"
date:  2026-01-25
categories: ["Lazy Bird Project"]
tags: []
---


## Introduction

You worked really hard last year and you finally can have some vacations and you decide to visit the hometown of your parents. You will visit your uncles, aunts, grandparents, and all sort of relatives that has not seen you and your parents for a long time. Whenever you meet a new relative they ask you: "How are your parents?" so, to provide the most adequate and trustful response you take your phone, call them and say: "Hey, Uncle José is asking how are you. How are you?". They answer you and you then answer your relative with: "They've just said that they are allright. Thank you". But this is getting ridiculous. You spent most of your time making calls to your parents that are also craving for some peace during your vacations and then you decide to make them a call early in every morning and keep the information for that day. Every single relative that ask you, will receive the same information, that will only be updated in the next morning. 

This is exactly how caching works. You get a piece of information, keep it with you for a specific amount of time that you found apropriated and give it to whomever asks you. After this specific amount of time expires, you then updates this information. 

## Caching

Caching is a brilliant solution and a powefull tool to make systems to run more efficiently. It relies on the speed of access of the intern memory of the system. Getting a value in memory is way faster than getting it from API calls, querying databases or from disk. So, the idea is to keep in memory chunks of data that are most commonly accessed and to update them accordingly. This "accordingly" means different for each kind of data but usually depends of which data we are handling.

### Why Does It Matter?

Caching matters because memory access is fast and cheap. Implementing it in your system means reducing a lot of I/O operation and latency and it's a key concept for efficient and scalable systems.

### Scenario

Whenever you have a data that is stale enough to keep in memory, is an indicative of caching possibility. Let's say we need to get some addresses related to people. We know that usually, under normal circustances, people don't use to move from their address every day, or month or maybe every year. Most of the people tends to live in the same address for years. So, if we have a system that exhibits people's address and we have a specific person that is really popular, we can cache their address and whenever a new request for their popular address is on the way, we can just look into the memory instead of calling an API or fetching the database.

## Problems

Caching has some interesting problems to be solved and strategies to be implemented. One of the most important is to understand how often your data changes in order to determine how often your cache will be updated. There are some cases that staleness is not a big deal.

Let's think about a weather app. There are a really few situations where a difference of few celsius would matter to the people. If you see that it's 20 C but it's 21 or 19, that's not a big deal. And we know that temperature is not changing too much in a period of one hour. So, we definitely can hit the Weather API just once every hour and cache the information for all the requests that are made in this period. 

 In other cases, the freshest the better and that caching will harm your system. Real Time systems, for example, can handle just a little or maybe zero caching. Applications to monitor traffic jam like Waze, must to show real time information to the users. So, it doesn't make sense to cache informations about crowded or empty streets, because it can change out of a suddenly and make the user really angry.
 
 So, to determine when and how to implement caching, you really need to understand not only your data but the user experience expected and how you will handle stale data. To make sure that your cache will provide good data, you need to implement some invalidation strategy. In this post, we won't get into too much details but we basically have these options: 

- As soon as you hit a value that is stale for more time than the expected (Time-To-Live TTL), fetches the API and refreshes the cache. 
- Create a async service that keeps looking for stale values and refreshing them.
- Etc.

## Conclusion

Cache is an indispensable concept and tool in software development and must be used whenever it is possible. We should have a deep knowledge of the nature of the data and the user experience that our system wants to provide so we can determine the best strategie to implement the caching and the right balance between stale and new data, without harms to the performance and latency of the system.

## Further Reading

If you want to learn more about it, you should visit these links:

-  
-  
-