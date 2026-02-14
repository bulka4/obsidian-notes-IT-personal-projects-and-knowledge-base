Tags: [[_Hive]] [[__Data_storage]] [[__Data_Engineering]]
#Hive #DataStorage #DataEngineering 

# Introduction
Hive Metastore is a data catalog which manages metadata for all Hive objects:
- Databases
- Tables and partitions ([[Spark - Data partitioning|link]])
- Columns and their data types
- Table locations (HDFS paths or object storage)

It uses a relational database like MySQL or PostgreSQL to store that metadata.

This metadata is used to compile SQL queries - decide how those queries will be executed (which data to load, from where).
# Compiling and running SQL queries
Hive Metastore doesn't compile nor run SQL queries. It only provides metadata needed for that.

HiveServer2 ([[Hive - HiveServer2|link]]) can compile SQL queries using metadata provided by Metastore and execute them using chosen engine (MapReduce, Tez, or Spark).
# Embedded and standalone modes
Embedded Metastore only works for single-user.

Remote/Standalone Metastore runs as a separate service for production, allows multiple clients (HiveServer2, Spark, Presto) to access metadata concurrently.
# Communication
Communication looks like that:
```yaml
Client (Beeline / BI Tool)
        |
        v
   HiveServer2
        |
        v
   Hive Metastore
        |
        v
Execution Engine (Spark / Tez / MapReduce)
        |
        v
   HDFS / Object Storage
```