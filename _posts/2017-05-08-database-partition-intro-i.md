---
layout: post
title: "Data base partition introduction I"
date: 2017-05-08
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

## Why partition
A data store hosted by a single server may be subject to limitations such as storage space, computing power, and network bandwidth. In some cases, data geolocation also matters. To improve scalability, manageability, performance, availability, security, and/or load balancing, large tables are splitted into smaller, individual tables.

There are two types of partition: vertical partition and horizonal partition (sharding).

## What is vertical partition/partition
Vertical partitioning involves creating tables with fewer columns and using additional tables to store the remaining columns. A common form of vertical partitioning is to split dynamic data (slow to find) from static data (fast to find) in a table where the dynamic data is not used as often as the static.

The two types of vertical partitioning are normalization and row splitting. 

Normalization is the standard database process of removing redundant columns from a table and putting them in secondary tables that are linked to the primary table by primary key and foreign key relationships. In this way, rows are collapsed into a single row to reduce space.

Row splitting divides the original table vertically into tables with fewer columns. Each logical row in a split table matches the same logical row in the other tables as identified by a UNIQUE KEY column that is identical in all of the partitioned tables. It leaves a one-to-one map between partitions; speeds up the access to large table by reducing its size.

Vertical partitioning scans less data and improved query performace, but it should be considered carefully, because analyzing data from multiple partitions requires queries that join the tables. Vertical partitioning also could affect performance if partitions are very large.

## What is horizontal partition/sharding
Horizontal partitioning divides a table into multiple tables that contain the same number of columns, but fewer rows.

Determining how to partition the tables horizontally depends on how data is analyzed. You should partition the tables so that queries reference as few tables as possible. Otherwise, excessive UNION queries, used to merge the tables logically at query time, can affect performance.

Note that there does not have to be a one-to-one correspondence between shards and the servers that host them: a single server can host multiple shards.

It can be difficult to maintain referential integrity and consistency between shards, so you should minimize operations that affect data in multiple shards.

## What is functional partition
I haven't seen functional partition concept else where other then Microsoft docs and *Cloud Design Pattern*.

For systems where it is possible to identify a bounded context for each distinct business area or service in the application, functional partitioning provides a technique for improving isolation and data access performance. Another common use of functional partitioning is to separate read-write data from read-only data that's used for reporting purposes.

## Another vertical and horizontal pair
In fact this is not related with the paritition topic, but it's interesting to see another pair of vertical/ horizonal definition.

Vertical Scaling is about adding more capability in the form of CPU and memory to existing machine or machines to enable improved responsiveness and availability of any system including database. In a virtual machine set up it can be configured virtually instead of adding real physical machines.

Horizontal Scaling is about adding more machines to enable improved responsiveness and availability of any system including database.The idea is to distribute the work load to multiple machines.

## Summary
Vertical table partitioning is mostly used to increase SQL Server performance especially in cases where a table with a lot of data that is not accessed equally, tables with data you want to restrict access to, or scans that return a lot of data.

Use sharding when a data store is likely to need to scale beyond the limits of the resources available to a single stor- age node and to improve performance by reducing contention in a data store.

## References
1. [Database table partitioning in SQL Server](https://www.sqlshack.com/database-table-partitioning-sql-server/)
2. [Partition (database)](https://en.wikipedia.org/wiki/Partition_(database))
3. [Horizonal VS vertical](http://stackoverflow.com/questions/20388923/database-partitioning-horizontal-vs-vertical-difference-between-normalizatio)
4. [Data partition](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning)
5. [Partition](https://technet.microsoft.com/en-us/library/ms178148(v=sql.105).aspx)