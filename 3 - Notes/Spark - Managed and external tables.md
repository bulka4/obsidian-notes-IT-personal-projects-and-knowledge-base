Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
Managed tables are tables whose data lifecycle is fully owned by Spark/Hive. Spark decides where the data is stored.
# Data storage location
In case of managed tables, data is saved automatically in the folder specified by the `spark.sql.warehouse.dir` configuration.
# Dropping tables
When we drop a table using the `DROP TABLE` command:
- In case of managed tables - both metadata and data gets deleted
- In case of external tables - only metadata gets deleted
# Creating a managed table
When we create a table without specifying a location where to save the data:
```SQL
CREATE TABLE sales (
  id INT,
  amount DOUBLE
);
```
then this table will become a managed table.
# Creating an external table
To create an external table, we need to provide a location where to save data and what format to use:
```SQL
CREATE TABLE sales_ext (
  id INT,
  amount DOUBLE
)
USING PARQUET
LOCATION 'abfss://data@account.dfs.core.windows.net/sales/';
```
