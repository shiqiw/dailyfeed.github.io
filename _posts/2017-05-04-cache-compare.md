---
layout: post
title: "In process cache VS distributed cache"
date: 2017-05-04
permalink: /specific/:year/:month/:day/:title
section: "specific"
---

Microsoft announced that on Nov 30, 2016, the In-Role Cache Service will no longer be supported. In role cache seems to be an Azure-specific term, elsewhere it is call in process cache. 

This write-up is just to make a not-in-depth discussion: is it always true that distributed cache is superior to in process cache?

## What is in process cache
Elements are cached local to a single instance of your application. 

[Post 1](https://msdn.microsoft.com/en-us/library/azure/hh914161.aspx) 
has some Azure specific explanation:

There are two main deployment topologies for In-Role Cache: co-located and dedicated. Co-located roles also host other non-caching application code and services. It is built by specifying a percentage of memory on each virtual machine to use for caching. Dedicated roles are worker roles that are only used for caching. It is only supported on worker roles and cannot be configured on web roles.

## What is distributed cache
All the following explanations come from [post 2](https://www.quora.com/What-is-distributed-caching#). 
Distributed caching refers to the ability in a distributed system to access data from within the distributed system itself instead of relying on a separate system of record.

Generally, the caching is performed in the main memory of the machines that make up the distributed system.

Information is typically replicated, partitioned (a.k.a. sharded), invalidated, or any combination thereof.

A distributed cache is accessed by primary key.

Information that is owned by other systems of record is typically accessed via a cache-aside model in which the application reads the data and then places it into the cache, or via a cache-through model in which the cache itself is responsible for communicating with the system of record.

## In process VS distributed
In process cache will be orders of magnitude faster than distributed cache because of network latency and object serialization.

However... in process cache may only guarantee eventual consistency while distributed cache is always consistent. Besides, distributed cache is expected to provide better reliability than in process cache, as a complete distributed cache failure should be degraded performance of the application as opposed to complete system failure, while this is not true for in process cache.

Once again, [post 3](http://stackoverflow.com/questions/26297511/performance-difference-between-azure-redis-cache-and-in-role-cache-for-outputcac) has a case analysis, that worth reading. 