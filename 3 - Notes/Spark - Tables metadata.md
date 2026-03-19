Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
In order to use Spark SQL to operate on tables from a Spark catalog ([[Spark - Catalog|link]]), we need metadata describing tables: their names, where they store data, column types etc.

When we want to execute a SQL query, we need to use that metadata to figure out how to execute that query.

For each catalog we specify separately where that metadata is stored and how it is used for executing SQL queries.

For storing and using metadata for executing SQL queries we can use such tools as:
- Hive Metastore ([[Hive - Metastore|link]])
- Iceberg ([[_Iceberg|link]])

So when Spark wants to execute a SQL query, it talks to those tools (e.g. Hive Metastore) and they retrieve the necessary metadata and prepares a plan for how to execute that query.