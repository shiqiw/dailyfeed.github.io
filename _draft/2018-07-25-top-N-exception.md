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

At first, we only need to know the exception name, but it would be optimum to know other details such as service name, exception detail including stack trace, and line number in file. Also, we'd like to minimize network traffic and other resource consumed by the syste.

### A few key words
Due to the high volume of exception request and performance requirement, we need to partition the request processing to achieve concurrency. Map/reduce method becomes a natural choice.

To avoid shipping data around, we do computation in single place. Hashing becomes useful here: with hash of exception signature, we achieve the goal of reduce payload size as well as implementing partition scheme based on exceptions (same exception always goes to same box).

Assuming only need to aggreaget top N exception from any given service is wrong - if there is load balancing that exception may go to different boxes. There can be situation where top N+mth exception on a given box come up among top N in the final tally. Barring rebalance (consistent hashing would only ensure exception type count not exception count is even), then same exception does not go to different boxes.

N+m scenario does not mean you need to take total tally of all exception, we allow trading accuracy for performance: 
1. You can set a threshold which means the count is too minor to be taken to final tally. 
2. In many real world system, they just set m value, such as m=N (i.e send top 2N exception from each box to merge). With larger N, there is more accuracy.

(Questionable) If you assume a fixed size of machines, and we have some way of identifying just the log records of past 24 hours efficiently (like daily log rotation or a time stamp index), then time complexity of just O(r) where r is the number of log records from the past 24 hours

### Reference
https://community.tableau.com/thread/156205
https://zpjiang.me/2017/11/13/top-k-elementes-system-design/
http://infolab.stanford.edu/~olston/publications/topk.pdf
https://www.aegissofttech.com/articles/how-to-get-top-n-words-count-using-big-data-hadoop-mapreduce-paradigm-with-developers-assistance.html
https://stackoverflow.com/questions/21692624/design-a-system-to-keep-top-k-frequent-words-real-time
https://acadgild.com/blog/mapreduce-design-pattern-finding-top-k-records
http://kamalnandan.com/hadoop/how-to-find-top-n-values-using-map-reduce/
https://www.quora.com/What-is-the-distributed-algorithm-to-determine-the-median-of-arrays-of-integers-located-on-different-computers