Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
Spark is the execution engine - responsible for query planning and execution while metadata store ([[Spark - Tables metadata|link]]) (like Iceberg or Hive metastore) is responsible only for providing Spark metadata needed to execute queries.
# Spark
Specifically, Spark handles:
- Parsing the SQL: Converts your SQL query into a logical plan.
- Query Optimization: Applies Catalyst optimizer rules to create a more efficient logical plan.
- Physical Planning: Decides how to execute the query across the cluster (e.g., which transformations to apply, joins, shuffles).
- Task Execution: Runs distributed tasks on the cluster to process data in parallel.

So Spark is essentially the “brain and muscles” of your query—it decides what to do and then actually does it across the cluster.
# Metadata store
Metadata store only provides Spark information needed to execute SQL queries like where tables data is stored.
# How they work together
Here’s a step-by-step picture of a SQL query execution:
1. SQL submitted → Spark parses SQL.
2. Logical plan creation → Spark asks metadata store: “Which files do I need for this query?”
3. Metadata store consults metadata → Returns only the relevant data files (file pruning, partition pruning).
4. Spark executes physical plan → Reads data from those files, applies filters, joins, aggregations, etc.
5. Results returned → Spark can also write back to metadata store, creating a new snapshot with ACID guarantees.
# Example
For example, when we use Spark with Iceberg ([[_Iceberg|link]]), Iceberg provides a functionality of data versioning - it saves information about different versions of data, how data changes in time ([[Iceberg - Introduction|link]]).

That allows to check how a table looked like in the past by running a query like this:
```sql
SELECT * FROM table VERSION AS OF 123
```

But still it is Spark which provides the functionality of data versioning and the `VERSION AS OF ...` command, and Spark executes it while Iceberg only provides metadata needed for it.