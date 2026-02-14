Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
In order to use Spark SQL, we need a catalog metadata ([[Data storage catalog|link]]). It provides metadata about tables (their names, where they store data, column types etc.) and it is needed to for SQL queries to work.

Spark can create by default an in-memory catalog which dies when SparkSession ends (metadata gets deleted).

To have a persistent metadata across sessions and also available for multiple sessions at once, we need to use an external metadata db like Hive Metastore ([[Hive - Metastore|link]]).