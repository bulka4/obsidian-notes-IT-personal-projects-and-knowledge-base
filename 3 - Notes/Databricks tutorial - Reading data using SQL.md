Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]], [[_Databricks]]

# Introduction
Once we saved data in a delta table format (we created folder with parquet files and delta_log folder), we can’t use sql in order to query it in a different notebook. At first we need to save additional metadata about those files in either Hive Metastore (legacy) or Unity Catalog (recommended). For that we can use sql commands:
```
%sql

drop table if exists delta_table;

-- create a table using data from the azure data lake. This will save table metadata in hive metastore or unity catalog

CREATE TABLE delta_table

USING DELTA

LOCATION 'abfss://<container name>@<storage account name>.dfs.core.windows.net/delta_tables/df';

-- read data from the table

SELECT * FROM delta_table
```
After using the ‘CREATE TABLE delta_table’ command we are creating metadata describing our table and now we can use sql in order to query that table, even in another notebook. So we need to use the ‘CREATE TABLE’ command only once, not every time we want to query our table.

#Cloud #MLEngineering #DistributedComputing #DataEngineering 