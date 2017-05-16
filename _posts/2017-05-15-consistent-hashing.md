---
layout: post
title: "Consistent hashing"
date: 2017-05-15
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

Last time, we mentioned that *consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key space to a size that can be listed*. Today, we are going to unveil consistent hashing.

## Concept of consistent hashing

Consistent hashing is a special kind of hashing such that when a hash table is resized, only K/n keys need to be remapped on average, where K is the number of keys, and n is the number of slots. 

The basic idea behind the consistent hashing algorithm is to hash both objects (resources) and caches (consumers) using the same hash function. In this way, the cache is mapped to an interval, which will contain a number of object hashes. If the cache is removed then its interval is taken over by a cache with an adjacent interval. All the other caches remain unchanged.

It has been used in distributed database, distributed hash tables and for reducing impact of partial system failures in large web applications.

## Implementation of consistent hashing

The hash function actually maps objects and caches to a number range. Imagine mapping this range into a circle so the values wrap around.

![Figure 1]({{ site.url }}/assets/consistent-hashing-1.png){:class="post-image"}

To find which cache an object goes in, we move clockwise round the circle until we find a cache point. So in the diagram above, we see object 1 and 4 belong in cache A, object 2 belongs in cache B and object 3 belongs in cache C. Consider what happens if cache C is **removed**: object 3 now belongs in cache A, and all the other object mappings are unchanged. If then another cache D is **added** in the position marked it will take objects 3 and 4, leaving only object 1 belonging to A.

![Figure 2]({{ site.url }}/assets/consistent-hashing-2.png){:class="post-image"}

There are chances that distribution of cache nodes over the ring is not uniform. This can be ameliorated by adding each cache node to the ring a number of times in different places. This is achieved by having a *num-tokens*, which applies to all caches in the ring, and when adding a cache, looping from 0 to the num-tokens – 1, and hashing a string made from both the cache and the loop variable to produce the position. This has the effect of distributing the caches more evenly over the ring. The new paradigm is called **virtual nodes**.

## Usage: partitioning

Cassandra chooses consistent hashing for purpose of even distribution of data, easy maintenance of balanced load across the nodes when a node is added or removed from set of nodes, and awareness of which node is responsible for a particular data.

Range partition has the disadvantage of requiring a table that maps ranges to instances. This table needs to be managed and a table is needed for every kind of object, so therefore range partitioning in Redis is often undesirable because it is much more inefficient than other alternative partitioning approaches. A few Redis cache clients and proxies implements consistent hashing as an advanced form of hash partitioning. 

Although partitioning in Redis is conceptually the same whether using Redis as a data store or as a cache, there is a significant limitation when using it as a data store. When Redis is used as a data store, a given key must always map to the same Redis instance. When Redis is used as a cache, if a given node is unavailable it is not a big problem if a different node is used, altering the key-instance map as we wish to improve the availability of the system.

If Redis is used as a cache scaling up and down using consistent hashing is easy.

If Redis is used as a store, a fixed keys-to-nodes map is used, so the number of nodes must be fixed and cannot vary.

## Usage: load balancing

## References
1. [Consistent hashing](https://en.wikipedia.org/wiki/Consistent_hashing)
2. [Consistent hashing](http://www.tom-e-white.com/2007/11/consistent-hashing.html)
3. [Consistent Hashing in Cassandra](https://blog.imaginea.com/consistent-hashing-in-cassandra/)
4. [Partitioning: how to split data among multiple Redis instances.](https://redis.io/topics/partitioning)

## Appendix

Java implementation of consistent hashing

```
import java.util.Collection;
import java.util.SortedMap;
import java.util.TreeMap;

public class ConsistentHash<T> {

  private final HashFunction hashFunction;
  private final int numberOfReplicas;
  private final SortedMap<Integer, T> circle =
    new TreeMap<Integer, T>();

  public ConsistentHash(HashFunction hashFunction,
    int numberOfReplicas, Collection<T> nodes) {

    this.hashFunction = hashFunction;
    this.numberOfReplicas = numberOfReplicas;

    for (T node : nodes) {
      add(node);
    }
  }

  public void add(T node) {
    for (int i = 0; i < numberOfReplicas; i++) {
      circle.put(hashFunction.hash(node.toString() + i),
        node);
    }
  }

  public void remove(T node) {
    for (int i = 0; i < numberOfReplicas; i++) {
      circle.remove(hashFunction.hash(node.toString() + i));
    }
  }

  public T get(Object key) {
    if (circle.isEmpty()) {
      return null;
    }
    int hash = hashFunction.hash(key);
    if (!circle.containsKey(hash)) {
      // Returns a view of the portion of this map whose keys are greater than or equal to fromKey.
      SortedMap<Integer, T> tailMap =
        circle.tailMap(hash);
      // FirstKey returns the first (lowest) key currently in this map.
      hash = tailMap.isEmpty() ?
             circle.firstKey() : tailMap.firstKey();
    }
    return circle.get(hash);
  } 

}
```