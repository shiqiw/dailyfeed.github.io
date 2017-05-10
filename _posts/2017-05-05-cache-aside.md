---
layout: post
title: "Cache aside"
date: 2017-05-05
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

Since we talked about different types of cache yesterday, it seems reasonable to know a little more about their usage patterns, thus cache aside pattern is today's topic.

## What is cache aside?
Application is responsible for reading and writing from the database and the cache doesn't interact with the database at all. The cache is "kept aside" as a faster and more scalable in-memory data store. The application checks the cache before reading anything from the database. And, the application updates the cache after making any updates to the database. This way, the application ensures that the cache is kept synchronized with the database.

## What is its benefit?
Drastically improve the performance of any database
application by avoiding expensive I/O operation for same data.

## What are potential issues?
Data consistency. This issue stands out for 1. private in process caches during repeated accesses that caches become inconsistent with each other quickly, and for 2. data store versus cache when synchronization occurs very frequently.

## When to/not to use it?
Announcement: ideas in this section are primarily from *Cloud Design Patterns*, which needs some further discussion.

Use it when:
- cache solution does not provide native read-through and write-through operations.
- resource demand is unpredictable.

Don't use it when:
- the cached data set is static (I assume CDN will be more useful in this case).
- For caching session state information in a web application hosted in a [web farm](https://en.wikipedia.org/wiki/Server_farm).

## What are other caching strategies?
Application treats cache as the main data store and reads data from it and writes data to it. The cache is responsible for reading and writing this data to the database, thereby relieving the application of this responsibility.

Read through
- Application reads the data from the cache. If the data is available in the cache application will get it, else application reads the data from the data store and store it in the cache for the future references.
- Objects in the cache are stored for a specific time. If a write happens to the object (in data store I assume) within that time frame and invalidates the cache, then next immediate read after the write will hit the data store and update the cache.

Read ahead
- Read the frequent access data from the data store, before the cache object get evicted. The refresh happens automatically while in the Read Through this refresh happens on demand.

Write through
- Applications write the data to the cache, not to the data store. The caching service will write the data transparently to the data store. Write operation returns a success when the data is written to the cache and to the data store. Since data is written to the cache, no need to invalidate the object. Modifications to the object in the cache need to be handled in a thread safe way (for example, reader-writer lock). 

Write around 
- Similar technique to write through, but write I/O is written directly to permanent data store, bypassing the cache. 

Write behind
- Application writes the data to the cache (and add into write behind queue). A write is considered success if the write to the cache is success. Either periodically or based on eviction time or based on any specific parameter, data store will be updated.

## A few comparisons:
Read through VS. read ahead
- Refresh-ahead reduces latency if objects are being accessed by a large number of users, but only if the cache can accurately predict which cache items are likely to be needed in the future.
- The higher the rate of inaccurate prediction, the greater the impact will be on throughput - potentially even having a negative impact on latency should the database start to fall behind on request processing.

Write through VS. write behind
- Write behind generally improves throughput, reduce database load (fewer writes) and cache server load (reduced cache value deserialization), insulate application from database failure to some extent and helps build linear scalability, however it needs at least one stage of master-slave model to be reliable. Besides, it misses auditing trails.

Read-Through/Write-Behind versus Cache-Aside
- Simplify application code. 
- Better read scalability by blocking parallel calls for same object. Auto-refresh cache on expiration or data base change.
- Better write performance because cache-aside updates are synchronous while write-behind is async.

## References
1. [Read-Through, Write-Through, Write-Behind, and Refresh-Ahead Caching](https://docs.oracle.com/cd/E15357_01/coh.360/e15723/cache_rtwtwbra.htm#COHDG5181)
2. [Write-through, write-around, write-back: Cache explained](http://www.computerweekly.com/feature/Write-through-write-around-write-back-Cache-explained)
3. [What's the advantage of Read-through, write-behind over cache-aside pattern in AppFabric?](http://stackoverflow.com/questions/25927436/whats-the-advantage-of-read-through-write-behind-over-cache-aside-pattern-in-a)
4. [Read-through & Write-through in Distributed Cache](http://www.alachisoft.com/resources/articles/readthru-writethru-writebehind.html)