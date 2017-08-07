---
layout: post
title: "Memcached"
date: 2017-08-06
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

## Why Memcached
1）对数据库的高并发读写：memcache使用多路复用I/O模型，多路复用I/O是一种消息通知模式，用户连接做好I/O准备后，系统会通知我们这个连接可以进行I/O操作，这样就不会阻塞在某个用户连接。因此，memcache才能支持高并发。

此外，memcache使用了多线程机制。可以同时处理多个请求。线程数一般设置为CPU核数，这研报告效率最高。

2）对海量数据的处理

## What is Memcached
保存在memcache中的对象实际放置在内存中。在实际使用中，通常把数据库查询的结果保存到Memcache中，下次访问时直接从memcache中读取，而不再进行数据库查询操作，这样就在很大程度上减少了数据库的负担。

基于libevent的事件处理，即使对服务器的连接数增加，也能发挥O(1)的性能。

使用Slab分配算法保存数据。删除过期item。使用LRU(last recently used)算法淘汰数据。

## Redis cache vs memcached
Read/write speed: Both are extremely fast.

Memory usage: Redis is better. memcached: You specify the cache size and as you insert items the daemon quickly grows to a little more than this size. redis: Setting a max size is up to you. Redis will never use more than it has to and will give you back memory it is no longer using.

Disk I/O dumping: A clear win for redis since it does this by default and has very configurable persistence.

Scaling: Both give you tons of headroom before you need more than a single instance as a cache.

Memcached is a simple volatile cache server. It allows you to store key/value pairs where the value is limited to being a string up to 1MB.

Redis can do the same jobs as memcached can, and can do them better.

Redis can act as a cache as well. It can store key/value pairs too. In redis they can even be up to 512MB.

You can turn off persistence and it will happily lose your data on restart too. If you want your cache to survive restarts it lets you do that as well. In fact, that's the default.

## Reference
1. [深入了解Memcached原理](http://blog.csdn.net/wusuopuBUPT/article/details/18238003)