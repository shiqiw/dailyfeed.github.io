---
layout: post
title: "Recent feeds"
date: 2017-11-14
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

### Browser based indexing
历史记录索引。

### 区块链
运用多种技术（去中心化的对等网络、密码学、时序数据和共识机制）来保证分布式数据库各节点的连贯和持续，使信息能即时验证、可追溯、难篡改、无法屏蔽。是一种共享价值体系。

### Apache Kafka
是一种分布式发布-订阅系统。

- 架构：Topic是特定类型的消息流。Producer发布payload到话题的对象。Broker（Kafka集群）是保存已发布的消息的一组服务器。Consumer可以订阅一个或者多个话题，从broker获取数据。一个卡夫卡集群通常有多个代理，将话题分成多个分区，每个代理存储一个或者多个分区。

- 存储：每个分区有一个段文件，消息追加到文件末尾。Id由逻辑偏移量加上消息长度计算。如果消费者知道特定的偏移量，则他已经消费了之前的信息。消费者的每个请求都需要包括逻辑偏移量。段文件一段时间或一定大小后写入磁盘。

- 代理：代理是无状态的，状态由消费者维护，因此消费者可以多次消费数据。

- ZooKeeper：在任意时间点确定哪些服务器活着且在工作中。本质是分布式分层级的文件系统。每个代理通过ZooKeeper协调其他代理。

### Rainbow table
Used to crack password hashes, exp plaintext password up to a certain length consisting of linited set of characters. Brute force attack. Trade off time and space.

Hashing and reduction function (any function that return 'plain text' value at given length). Repeat H and R process, if it falls into a chain endpoint, we have the start point and recreate the chain. If it contains value we have, then the immediate predecessor is the password we are looking for.

Simple hash chain may collide. Reduction function is hard to choose. Rainbow table replace simple R with a set of R[k]. Remove duplicate chain that have same final value. These chains may overlap briefly, but will not merge.

```
Still need to understand why it takes k times more space with k times less time
```

But with large saltes, rainbow table will not work well. Other efforts include key strengthening, key stretching...