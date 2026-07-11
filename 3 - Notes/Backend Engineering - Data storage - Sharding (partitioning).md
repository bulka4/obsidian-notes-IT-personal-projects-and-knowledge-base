Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Sharding (also called partitioning) is a technique for splitting data across multiple machines so that no single server has to store or process everything. Its goal is to improve scalability.
# Shards / partitions
Data on each server is called a shard / partition.
# How it works
Instead of storing everything on a single server, we split the data so each server stores only a part of it. For example, we can store data for different users on different servers:
```
Shard 1:
Users 1...250,000

Shard 2:
Users 250,001...500,000

Shard 3:
Users 500,001...750,000

Shard 4:
Users 750,001...1,000,000
```
# Partition routing
The application needs to know which shard contains a specific data which it is looking for. This is called partition routing.
# Partitioning strategies
- Range partitioning - [[Backend Engineering - Sharding (partitioning) - Range partitioning|link]] 
- Hash partitioning - [[Backend Engineering - Sharding (partitioning) - Hash partitioning|link]] 
 - Directory-based partitioning - [[Backend Engineering - Sharding (partitioning) - Directory-based partitioning|link]] 
 - Consistent hashing - [[Backend Engineering - Sharding (partitioning) - Consistent hashing|link]] 
# Rebalancing
As data grows, it might become distributed unequally, for example:
```
Shard 1 = 2 TB
Shard 2 = 2 TB
Shard 3 = 20 TB
```

In this case, we need to move data between shards to balance it. This is called **rebalancing**.
# Hot partition problem
A hot partition problem is a problem where one shard is much more overloaded (there is a high traffic for it, a lot of reads and writes).

For example, on social platforms, data about celebrities might be frequently read.