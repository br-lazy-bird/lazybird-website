---
title: "First Broken System Complete"
date:  2025-10-01 13:15:12
categories: ["Lazy Bird Project"]
tags: []
---

The first broken system is finally complete. It took slightly longer than expected because I wanted to build a solid foundation for future systems. There was also a lot to learn and adapt along the way. This first iteration took 15 days from issue creation to completion, plus about a week of planning and GitHub setup and issues creation.

[You can see it here on GitHub.](https://github.com/br-lazy-bird/lazy-bird)

## Learnings

### Performance Consistency Challenges

When I first ran the performance test on my machine (MacBook Air M4 16GB) I got a decent performance even without the table indexes. It made me think about how different machines would impact my idea. So I decided to cap the resources through the Docker configurations to get a poorer performance and a way to provide a consistent environment between users with different machines. 

On my local machine, without any indexes or customizations, I got P50 of 13 ms and P99 of 18 ms. With the custom resource configurations, I got P50 of 295 ms and P99 of 401 ms.

### Frontend Design Choices

I had some back-and-forth about how the frontend for this first project should work. Initially, I considered just having a button that would hit an endpoint performing a single query. However, even with limited Docker resources and no index, it was too fast. Users would not have a clear perception of the poor performance. So, I decided to create a performance test that runs 100 queries and provides performance metrics. This wasn't what I originally envisioned. My goal was to showcase the issue in an application as close to a real one as possible. But for this specific case, since I didn't want to add unnecessary complexity, the performance test met the needs.

### Real-Time Progress with Server-Sent Events

In order to showcase the progress of the performance test, I decided to implement a progress bar in the frontend. I already had implemented the endpoint that streamed the data related to each query execution, so the progress bar should be straightforward.

However, it didn't work. Although the endpoint was working properly, the frontend waited for the final event before handling all at once, preventing the progress bar from working. After some investigation, I found the problem was the React proxy buffering events. Development proxies can buffer SSE streams, so I needed to write a custom setup for the React proxy or to connect directly to the backend URL instead of using the proxy. The fastest and easiest solution was connect directly to the backend URL.


### Testing Infrastructure Insights

Initially, I planned to have a fully tested system, treating it like a production system. However, since this first broken system executes only a single action, a wide test suite became less important. It's a working system where the user performs a single database change and the code itself won't even be modified. I also considered measuring the improvement's impact using performance tests to verify whether indexes were added. But this would give clues to the user, and I wanted to give them the opportunity to identify and fix the problem on their own. I would have spent time developing something that wouldn't add value to the learning experience. 


