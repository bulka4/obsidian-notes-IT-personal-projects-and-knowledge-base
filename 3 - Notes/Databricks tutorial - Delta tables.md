Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]], [[_Databricks]]

# Introduction
Delta table is a format for storing tabular data. It stores data for one table in a bunch of files (for example csv. It can be one or multiple files) in a folder.

There is also a delta_log folder which keeps transaction logs. Those logs contain information about all the changes we made to a table. It allows for example to go back in time to check how a table looked like before. It also allows for efficient modifications of a table like inserting, modifying or deleting rows or columns.

Delta tables allow for quick querying. It stores data in a column oriented way, like in sql server when you are using indexes.
## How to create a delta table
In order to create a delta table we need to create a folder with parquet files which contain data and a delta_log folder in which there will be saved transaction logs.

At first we need to created a dataframe using for example this command:
```
df = spark.read.csv("abfss://<container name>@<storage account name>.dfs.core.windows.net/<path to csv file>")
```
Then we can save it in Azure Data Lake in a delta table format using this command:
```
df.write.format("delta")
  .mode(SaveMode.Overwrite) // Choose appropriate SaveMode (Overwrite, Append, etc.)
  .save("abfss://<container name>@<storage account name>.dfs.core.windows.net/<path to a folder>")
```
So that code will create a folder with parquet files and a delta_log folder.

#Cloud #MLEngineering #DistributedComputing #DataEngineering 