---
layout: post
title: "Data base partition introduction II"
date: 2017-05-14
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

We roughly talked about what data base partition is, and partioning methods a couple of days before. Today, we will extend our discussion to sharding criteria because splitting the data in a way that is appropriate for the types of queries the application performs ensures optimal performance and scalability.

## Partition key /shard key
Partition key or shard key, however you call it, is one or more attributes of the data whcih is used to determine which shard should you to the data to. The shard key should be static. It should not be based on data that might change.

In MongoDB, the shard key is either an indexed field or indexed compound fields that exists in every document in the collection.

In Cassandra, partition key is the first column declared in the PRIMARY KEY definition, or in the case of a compound key, multiple columns can declare those columns that form the primary key.

## Partition criteria

**Round-robin partitioning**

The simplest strategy, it ensures uniform data distribution. With n partitions, the ith tuple in insertion order is assigned to partition (i mod n). 

This strategy enables the sequential access to a relation to be done in parallel. However, the direct access to individual tuples, based on a predicate, requires accessing the entire relation.

**Range partitioning**

Selects a partition by determining if the partitioning key is inside a certain range. It is adopted by MongoDB.

In addition to supporting exact-match queries (as in hashing), it is well-suited for range queries. This strategy is friendly to scaling and data movement. 

With the benefit of easy to implement, supporting for rage query and easy data management, it may not provide optimal balancing between shards. Rebalancing the shards is difficult.

**List partitioning**

It is also called "lookup strategy". A partition is assigned a list of values. If the partitioning key has one of these values, the partition is chosen. 

Using virtual shards reduces the impact when rebalancing data because new physical partitions can be added to even out the workload, but looking up shard locations can impose an additional overhead. It has some limitation for scaling and data movement.

**Hash partitioning**

Applies a hash function to some attribute that yields the partition number. This strategy allows exact-match queries on the selection attribute to be processed by exactly one node and all other queries to be processed by all the nodes in parallel. 

The purpose of this strategy is to reduce the chance of hotspots in the data.

With better chance of a more even data and load distribution using this trategy, computing the hash may impose an additional overhead. Rebalancing shards is difficult as well. Scaling and data movement is complex here.

**Composite partitioning**

Allows for certain combinations of the above partitioning schemes, by for example first applying a range partitioning and then a hash partitioning. Consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key space to a size that can be listed.

## References
1. [Shard keys](https://docs.mongodb.com/manual/core/sharding-shard-key/)
2. [Compound keys and clustering](http://docs.datastax.com/en/cql/3.1/cql/ddl/ddl_compound_keys_c.html)
3. [Difference between partition key, composite key and clustering key in Cassandra?](http://stackoverflow.com/questions/24949676/difference-between-partition-key-composite-key-and-clustering-key-in-cassandra)
4. [Partition (database)](https://en.wikipedia.org/wiki/Partition_(database))