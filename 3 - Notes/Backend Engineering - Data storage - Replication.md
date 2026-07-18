Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Replication is a practice of keeping multiple copies of the same data or service state on different machines (nodes) so that the system can survive failures, improve performance, or scale.
# Usecases
We use it for:
- Availability - When one node fails, others still contain the data
- Performance - A single database may become overloaded so we can distribute reads across replicas
- Geographic distribution - We place databases in different places on Earth and users takes data from the database closest to them
# Types of replication
## 1. Leader-Follower Replication (Primary-Replica)
- This is the most common model.
- One node is the leader (primary/master).
- Other nodes are followers (replicas/slaves).
- The leader processes operations (INSERT, UPDATE, DELETE), then sends changes to replicas.
## Single leader
Most common.

Examples:
- PostgreSQL streaming replication
- MySQL replication
- MongoDB replica sets

Structure:
```
        Leader
       /  |  \
      R1  R2  R3
```

Advantages:
- simple
- easy writes

Problems:
- leader is bottleneck
## 2. Multi-leader replication
Multiple nodes accept writes.

Example:
```
        USA DB
          |
          |
       replicate
          |
          |
       EU DB
```

Users in Europe write to Europe.  
Users in America write to America.

Advantages:
- low latency globally

Problem are conflicts (different replicas will have different data). For example:

USA replica stores a write:
```
username = John
```

Europe replica stores a write:
```
username = Mike
```

Which value wins? We need to use some conflict resolution method ([[Backend Engineering - Distributed systems - Conflict resolution|link]]).
## 3. Leaderless replication
Used by systems like Apache Cassandra and some distributed databases.

No primary.

Every node accepts writes:
```
      Client
        |
   -------------
   |     |     |
  DB1   DB2   DB3
```

A write may go to all nodes:
```
SET x = 10

DB1: x=10
DB2: x=10
DB3: x=10
```

Reads may query multiple nodes and compare results.
# Synchronous vs asynchronous replication
## Asynchronous replication
The leader does not wait. A user gets a response immediately.

Advantages:
- fast
- high throughput

Problem: a replica may be behind (it doesn't contain the latest data). This is called a replication lag.
## Synchronous replication
The leader waits until replicas confirm.

Advantages:
- stronger consistency (all the replicas has the same data)

Problems:
- slower
- one slow replica can slow everything
# Quorum replication
Leaderless systems often use quorum rules. In this technique, writes and reads go to a specific number of nodes:
- W - number of nodes for writes
- R - number of nodes for reads

If R + W > N, where N is a total number of nodes, then there is always at least one node from which we can read the latest data because it can be used for both read an write, and:
- Because it is used for write, it contains the latest data
- Because it is used for read, we can read that latest data
# Replication logs
Most real systems replicate **operations**, not entire databases. Instead of copying an entire database, they use a log of operations, for example:
```
1. INSERT user 10
2. UPDATE balance
3. DELETE order 55
```

and each replica replicates those operations.
# Questions
- How does the Quorum replication work, why there is always at least one node with the newest value?