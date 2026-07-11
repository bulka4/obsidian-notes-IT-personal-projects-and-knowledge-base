Tags: [[_Databases]]
#Databases  

# Introduction
A storage engine is the component of a database responsible for physically storing, retrieving, and modifying data on disk and in memory.

We can think of it as:
```
SQL Layer
- SQL parser
- Query optimizer
- Transaction manager
        |
        v
Storage Engine
- stores rows
- manages indexes
- caching
- locking
- logging
- recovery
```

The SQL layer decides:
> "I need rows where `user_id = 123`."

The storage engine decides:
> "How do I actually find these rows on disk efficiently?"
# Responsibilities of a storage engine
Storage engines determine:
- read performance
- write performance
- transaction capabilities
- compression
- scalability
- recovery after crashes
- indexing possibilities

They usually implement:
## Data storage format
How rows are physically stored:
```
Disk
|
+-- pages
     |
     +-- rows
```
## Indexes
Indexes are data structures that make reading / writing data faster.

Examples:
- B-Trees
	- Optimized for:
		- Point lookups
		- Range queries
		- Mixed reads/writes
- Hash indexes
- LSM Trees
	- Optimized for very high write throughput
## Caching
Frequently accessed pages may remain in memory.
## Transactions
- WAL
- MVCC
- locking
- recovery after crashes
## Compression
Compressing stored data.
## Concurrency control
Handling many users reading/writing simultaneously.
# Why are storage engines important?
Different workloads need different optimizations.

Example:
## OLTP workload
Many small operations:
```
Get user
Update balance
Insert order
```

Needs:
- low latency
- many writes
- transactions
## Analytics workload
Queries:
```sql
SELECT SUM(revenue)
GROUP BY country;
```

Needs:
- reading large amounts of data
- compression
- sequential scans

These workloads may prefer different storage engines.
# Row storage vs column storage
## Row-oriented
Values from the same row are stored together on a disk:
```
Row1:
Alice,30,Poland

Row2:
Bob,25,Germany
```

It makes it efficient to retrieve or update complete records (with all the columns). It is good for OLTP systems where we select many columns, for example:
```sql
SELECT *
FROM users
WHERE id=123;
```
## Column-oriented
Values from the same column are stored together on a disk:
```
Names:
Alice
Bob

Ages:
30
25
```

It makes it efficient to read only selected columns and perform aggregations:
```sql
SELECT AVG(age)
FROM users;
```
