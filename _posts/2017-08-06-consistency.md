---
layout: post
title: "Consistency"
date: 2017-08-06
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

## Client side consistency
> Cloud consistency may diff database consistency.
>
> 1. Strict consistency: as if one copy.
>
> 2. Read your write consistency / local consistency: see his own updates immediately, but not guranteed for others' writes.
>
> 3. Session consistency: within same session ID, as if you are reading local cache.
>
> 4. Monotonic read consistency: you will only see more udpated version future request.
>
> Weak consistency: memcache; after a write, user may or may not see it. (Maybe need to guarantee lower version updates should not overwrite higher udpates...次序保证)
>
> Strong consistency: after a write, read will see it; RDBMS, Azure table, file system/
>
> Eventual consistency: arrange sequence, after a write, read will eventually see it; DNS, email.

## Server side consistency
> R + W > N ==> strong consistency
>
> R + W <= N ==> eventual consistency

## Back up
> Make a copy: check point snapshot, incremental back up ==> but does not guarantee snapshot contains latest update.
>
> Weak consistency.
>
> Usually no transaction. Like secondary backup primary.

## Master / slave replication
> Usually async, used in most RDBMS
>
> Weak / eventual consistency.
>
> In master / slave, if want to fault tolerant, need to have slave write commit before commit write to client, which means cannot batch request.

## Master / master replication
> Async, eventual consistency
>
> Need serialization protocol. 比如去Zoo Keeper里面拿一个global sequence ID或者实现global clock。
>
> 无论是master slave还是master master，在cloud里面都不支持互锁。在数据库实现的时候可能需要。

## Two phase commitment
> For each proposal, asking for agreement for all voters. It is semi-distributed, poor throughput.
>
> propose => vote (write propose to commit) => commit / abort (write a revert log)
>
> 3PC buys async with one extra round trip

### Paxos
> Fully distributed consensus protocol
>
> Majority write; survive minority failure; coordinayte moving state; not locking system.
>
> Memcache NoSQL DB协议，应该是没有使用Paxos。

### Compensating transaction
> Write transaction / operation log (instead of status), consolidate later (replay) to remove perf bottle neck.
>
> E.g ticket master should not access DB for each transaction. Pre-prequest certain amount of tokens, process them, consolidate and write to master; as one iteration. May lead to over book...
>
> Event sourcing pattern
