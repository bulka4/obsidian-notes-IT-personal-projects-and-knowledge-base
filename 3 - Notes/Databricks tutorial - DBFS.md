Tags: [[__Cloud]], [[__Machine_Learning_Engineering]], [[__Distributed_computing]], [[__Data_Engineering]], [[_Databricks]]

# Introduction
DBFS stands for databricks file system. This file system is on cluster of nodes (servers) which are making computations from our notebooks’ code and we can save there our data and files. We can access it by using dbutils.fs commands in notebooks, for example:
- remove files from a folder: dbutils.fs.rm(folder_path, True)
- list files from a folder: dbutils.fs.ls(folder_path)

#Cloud #MLEngineering #DistributedComputing #DataEngineering 