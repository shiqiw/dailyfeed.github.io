---
layout: post
title: "SQL compare"
date: 2017-08-05
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

An introduction of commonly used relational databases, namely SQLite, MySQL and PostgreSQL.

## Keyword: RDBMS
This is abbreviation for relational database management system. Similar we know there is DBMS in general.

Databases are logically modelled storage spaces for all kinds of different information. Each database, other than schema-less ones, have a model. These management systems implements relational model for use.

## SQLite
Keyword for SQLite is embedded, fast, self-contained and file-based.

The entire database consists of a single file on the disk, which makes it extremely portable.

Great for developing and even testing: can scale for concurrency.

No user management.

Lack of possibility to tinker with for additional performance: it is technically not possible to make it more performant than it already.

Use it when: All applications that need portability, that do not require expansion, e.g. single-user local applications, mobile applications or games. Applications that need to read/write files to disk directly. Testing.

Do not use it when: Multi-user applications. Applications requiring high write volumes.

## MySQL
Most common one. Despite not trying to implement the full SQL standard, MySQL offers a lot of functionality to the users.

Easy to work with. Feature rich. Secure. Scalable and powerful. Speedy.

Reliability issues. 

Use MySQL when: Distributed operations. High security. Web-sites and web-applications (flexible and somewhat scalable tool). Custom solutions.

Do not use MySQL when: SQL compliance. Concurrency (concurrent read-writes can be problematic). Lack certain features, such as the full-text search.

## PostgreSQL
PostgreSQL is the advanced, open-source [object]-relational database management system which has the main goal of being standards-compliant and extensible.

An open-source SQL standard compliant RDBMS. Extensible. Objective.

Bad performance for read-heavy operations. It is harder to come by hosts or service providers that offer managed PostgreSQL instances.

Use PostgerSQL when: Data integrity. Complex, custom procedures. Integration. Complex designs.

Not use PostgreSQL when: If all you require is fast read operations, PostgreSQL is not the tool to go for. Simple set ups. Replication.

## Reference
1. [SQLite vs MySQL vs PostgreSQL: A Comparison Of Relational Database Management Systems](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems)

2. [Understanding SQL And NoSQL Databases And Different Database Models](https://www.digitalocean.com/community/tutorials/understanding-sql-and-nosql-databases-and-different-database-models)