Current high end relational database management systems provide for different criteria to split the database. They take a partitioning key and assign a partition based on certain criteria. Common criteria are:

Range partitioning 
Selects a partition by determining if the partitioning key is inside a certain range. 
In addition to supporting exact-match queries (as in hashing), it is well-suited for range queries. For instance, a query with a predicate “A between A1 and A2” may be processed by the only node(s) containing tuples.

List partitioning 
A partition is assigned a list of values. If the partitioning key has one of these values, the partition is chosen. For example, all rows where the column Country is either Iceland, Norway, Sweden, Finland or Denmark could build a partition for the Nordic countries.

Composite partitioning 
Allows for certain combinations of the above partitioning schemes, by for example first applying a range partitioning and then a hash partitioning. Consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key space to a size that can be listed.

Round-robin partitioning 
The simplest strategy, it ensures uniform data distribution. With n partitions, the ith tuple in insertion order is assigned to partition (i mod n). This strategy enables the sequential access to a relation to be done in parallel. However, the direct access to individual tuples, based on a predicate, requires accessing the entire relation.

Hash partitioning 
Applies a hash function to some attribute that yields the partition number. This strategy allows exact-match queries on the selection attribute to be processed by exactly one node and all other queries to be processed by all the nodes in parallel.

## partition technique
https://intellipaat.com/blog/database-partitioning-techniques/
https://code.mixpanel.com/2011/05/11/sharding-techniques/

Horizontal Scaling:

is about adding more machines to enable improved responsiveness and availability of any system including database.The idea is to distribute the work load to multiple machines.

Vertical Scaling:

is about adding more capability in the form of CPU,Memory to existing machine or machines to enable improved responsiveness and availability of any system including database.In a virtual machine set up it can be configured virtually instead of adding real physical machines.

pros and cons of database partition, sharding and partition