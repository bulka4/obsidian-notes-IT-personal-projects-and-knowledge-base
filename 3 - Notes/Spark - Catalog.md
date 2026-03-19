Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
A catalog is a logical group of tables. Every table we create using Spark SQL is saved in some Spark catalog. A catalog contains schemas and schemas contains tables.

For every catalog we define:
- Where data of tables from that catalog is stored
- How table metadata ([[Spark - Tables metadata|link]]) is stored and managed (used to execute SQL queries)
	- Which tool is used for handling metadata, for example Hive Metastore ([[Hive - Metastore|link]]) or Iceberg ([[_Iceberg|link]])
# Default catalog
By default Spark creates the `spark_catalog` catalog which is an in-memory catalog (metadata is stored in memory during a Spark session. When session is finished, metadata is lost.)

Data from this catalog is stored at the location specified by the `spark.sql.warehouse.dir` config.