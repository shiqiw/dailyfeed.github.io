---
layout: post
title: "Top N Exceptions"
date: 2018-07-23
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

### Overview
Recently I gave this question in interview design module. There are some related design decisions and technologies that worth discussion.

### Question
There are multiple services. Each of them is running on hundreads of machines. For service monitoring purpose, we need to know what the most frequent N exceptions are in last hour/day/... 

Describe the system that provide data like this. Perferably not to touch the monitored service too much.

At first, we only need to know the exception name, but it would be optimal to know other details such as service name, exception detail including stack trace, and line number in file. Also, we'd like to minimize network traffic and other resource consumed by the syste.

### A few key words
In a small scale, top N problems can be easily solved using heap or bucket sort.

Due to the high volume of exception request and performance requirement, we need to partition the request processing to achieve concurrency. Map/reduce method becomes a natural choice.

To avoid shipping data around, we do computation in single place. Hashing becomes useful here: with hash of exception signature, we achieve the goal of reduce payload size as well as implementing partition scheme based on exceptions (same exception always goes to same box).

Assuming only need to aggreaget top N exception from any given service is wrong - if there is load balancing that exception may go to different boxes. There can be situation where top N+mth exception on a given box come up among top N in the final tally. Barring rebalance (consistent hashing would only ensure exception type count not exception count is even), then same exception does not go to different boxes.

N+m scenario does not mean you need to take total tally of all exception, we allow trading accuracy for performance: 
1. You can set a threshold which means the count is too minor to be taken to final tally. 
2. In many real world system, they just set m value, such as m=N (i.e send top 2N exception from each box to merge). With larger N, there is more accuracy.

(Questionable) If you assume a fixed size of machines, and we have some way of identifying just the log records of past 24 hours efficiently (like daily log rotation or a time stamp index), then time complexity of just O(r) where r is the number of log records from the past 24 hours

### Quick sort
Suppose you have a master node (or are able to use a consensus protocol to elect a master from among your servers).  The master first queries the servers for the size of their sets of data, call this n, so that it knows to look for the k = n/2 largest element.

The master then selects a random server and queries it for a random element from the elements on that server.  The master broadcasts this element to each server, and each server partitions its elements into those larger than or equal to the broadcasted element and those smaller than the broadcasted element.

Each server returns to the master the size of the larger-than partition, call this m.  If the sum of these sizes is greater than k, the master indicates to each server to disregard the less-than set for the remainder of the algorithm.  If it is less than k, then the master indicates to disregard the larger-than sets and updates k = k - m.  If it is exactly k, the algorithm terminates and the value returned is the pivot selected at the beginning of the iteration.

If the algorithm does not terminate, recurse beginning with selecting a new random pivot from the remaining elements.

Analysis:

Let n be the total number of elements and s be the number of servers.  Assume that the elements are roughly randomly and evenly distributed among servers (each server has O(n/s) elements).  In iteration i, we expect to do about O(n/(s*2^i)) work on each server, as the size of each servers element sets will be approximately cut in half (remember, we assumed roughly random distribution of elements) and O(s) work on the master (for broadcasting/receiving messages and adding the sizes together).  We expect O(log(n/s)) iterations.  Adding these up over all iterations gives an expected runtime of O(n/s + slog(n/s)), and assuming s << sqrt(n) which is normally the case, this becomes simply (O(n/s)), which is the best you could possibly hope for.

Note also that this works not just for finding the median but also for finding the kth largest value for any value of k.

### Count-Min Sketch + Heap
There are many ways to perform approximate calculation, Count-Min Sketch is one of them.

Assume that we have d hash functions, create a hash table T with d rows and m cols.

For each item read from data stream, get its hash values from d hash functions and perform mod operations respectively by m. Increase the value by one for each position T[hash_func][hash_value], we call it sketch.

When we want to query the frequency of a particular item, we get its d sketches, return the smallest sketch. As a matter of fact, each of the sketch can be used as its approximate frequency, here we use the minimum sketch.

The idea behind Sketch is very similar to Bloom Filter, they both use multiple hashing functions to resolve conflicts. The space complexity for Count-Min Sketch is O(dm), the time complexity is O(n).

The advantage of Count-Min Sketch is it saves massive space cost, making it possible to store stream data in memory. The disadvantage is, for those items with low frequency, the min sketch has a higher chance to represent a high frequent items, not low frequent items. However, what we care here is top frequent items, not top least frequent items.

### Lossy Counting
Lossy Counting Algorithm is another approximate algorithm to identify elements in a data stream whose frequency count exceed a user-given threshold. Let’s start with a simple example.

Step 1: Build a HashMap to store the mapping from element to its frequency.

Step 2: Build a data frame (window). (Split data into chunks)

Step 3: Read data from stream and put them in the data frame, get all their frequencies f and minus 1.)

Step 4: Update the item frequencies to HashMap, remove the items whose frequency equals to 0 from the HashMap.

Step 5: Repeat Step 3.

The basic idea is, it is less possible for a high frequent item to get removed from the map even though all of them have to be decreased by one for each round. As we read more data, low frequent items will be removed from HashMap and high frequent items stay.

### Reference
1. [Top K elements system design](https://zpjiang.me/2017/11/13/top-k-elementes-system-design/)
2. [Design a system to keep top k frequent words real time](https://stackoverflow.com/questions/21692624/design-a-system-to-keep-top-k-frequent-words-real-time)
3. [MapReduce Design Pattern – Finding Top-K Records](https://acadgild.com/blog/mapreduce-design-pattern-finding-top-k-records)
4. [MapReduce Implementation](http://kamalnandan.com/hadoop/how-to-find-top-n-values-using-map-reduce/)
5. [Distributed algorith to find kth largest element](https://www.quora.com/What-is-the-distributed-algorithm-to-determine-the-median-of-arrays-of-integers-located-on-different-computers)

Essay: http://infolab.stanford.edu/~olston/publications/topk.pdf