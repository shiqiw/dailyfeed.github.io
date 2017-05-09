---
layout: post
title: "Data base partition introduction I"
date: 2017-05-08
permalink: /specific/:year/:month/:day/:title
section: "specific"
---

## Why partition
A data store hosted by a single server may be subject to limitations such as storage space, computing power, and network bandwidth. In some cases, data geolocation also matters. To improve scalability, manageability, performance, availability, security, and/or load balancing, large tables are splitted into smaller, individual tables.

There are two types of partition: vertical partition and horizonal partition (sharding).

## What is vertical partition/partition
Vertical partitioning involves creating tables with fewer columns and using additional tables to store the remaining columns. A common form of vertical partitioning is to split dynamic data (slow to find) from static data (fast to find) in a table where the dynamic data is not used as often as the static.

Typical partition strategies include normalization (collapse rows into a single row to reduce space) and row splitting ( leave a one-to-one map between partitions; speed up the access to large table by reducing its size).

## What is horizontal partition/sharding
Horizontal partitioning divides a table into multiple tables that contain the same number of columns, but fewer rows.

Sharding strategies include lookup strategy (build mapping between the shard key and the physical/virtual storage), range strategy (group and order by shard key), and hash strategy (reduce the chance of hotspots).

## What is functional partition
I haven't seen functional partition concept else where other then Microsoft docs and *Cloud Design Pattern*.

For systems where it is possible to identify a bounded context for each distinct business area or service in the application, functional partitioning provides a technique for improving isolation and data access performance. Another common use of functional partitioning is to separate read-write data from read-only data that's used for reporting purposes.

## Use cases
Vertical table partitioning is mostly used to increase SQL Server performance especially in cases where a table with a lot of data that is not accessed equally, tables with data you want to restrict access to, or scans that return a lot of data.

Use sharding when a data store is likely to need to scale beyond the limits of the resources available to a single stor- age node and to improve performance by reducing contention in a data store.

## References
1. [Database table partitioning in SQL Server](https://www.sqlshack.com/database-table-partitioning-sql-server/)
2. [Partition (database)](https://en.wikipedia.org/wiki/Partition_(database))
3. [Horizonal VS vertical](http://stackoverflow.com/questions/20388923/database-partitioning-horizontal-vs-vertical-difference-between-normalizatio)
4. [Data partition](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning)