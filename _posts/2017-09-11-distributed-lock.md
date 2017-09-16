---
layout: post
title: "Distributed lock manager"
date: 2017-09-11
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

### What is Distributed Lock Manager?
A DLM provides software applications which are distributed across a cluster on multiple machines with a means to synchronize their accesses to shared resources. 

For efficiency: Taking a lock saves you from unnecessarily doing the same work twice. If the lock fails and two nodes end up doing the same piece of work, the result is a minor increase in cost.

For correctness: Taking a lock prevents concurrent processes from stepping on each others’ toes and messing up the state of your system.

### How to do distributed locking
Making the lock safe with fencing: include a fencing token with every write request to the storage service. (because processes may pause for arbitrary lengths of time, packets may be arbitrarily delayed in the network, and clocks may be arbitrarily wrong)

### VMS Implementation
DEC's VMS (virtual memory system) was the first widely available operating system to implement a DLM.

The DLM uses a generalized concept of a resource, which is some entity to which shared access must be controlled.

There are six lock modes that can be granted, and these determine the level of exclusivity being granted, it is possible to convert the lock to a higher or lower level of lock mode. When all processes have unlocked a resource, the system's information about the resource is destroyed.

A process can obtain a lock on a resource by enqueueing a lock request.

A lock value block is associated with each resource. This can be read by any process that has obtained a lock on the resource (other than a null lock) and can be updated by a process that has obtained a protected update or exclusive lock on it. It can be used to hold any information about the resource that the application designer chooses. A typical use is to hold a version number of the resource. 

The OpenVMS DLM periodically checks for deadlock situations.

### Google Chubby lock service
Google has developed Chubby, a lock service for loosely coupled distributed systems.

Chubby is a relatively heavy-weight system intended for coarse-grained locks, locks held for "hours or days", not "seconds or less."

### Apache Zookeeper
[Distributed Lock using Zookeeper](https://dzone.com/articles/distributed-lock-using)

### Deadlock condition
1. Mutual Exclusion

2. Hold and Wait

3. No Preemption

4. Circular Wait

### Reference
1. [Distributed Lock Manager](https://en.wikipedia.org/wiki/Distributed_lock_manager)

2. [Necessary conditions for deadlock](http://wikieducator.org/Necessary_conditions_for_deadlock)

3. [How to do distributed locking](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html)

4. [Chubby: The Google distributed lock manager](http://glinden.blogspot.com/2006/09/chubby-google-distributed-lock-manager.html)