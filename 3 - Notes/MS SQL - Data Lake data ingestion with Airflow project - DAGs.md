Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
There is one DAG (`dag/project_1/data_ingestion_dag.py`) which is ingesting data from the MS SQL database into the Azure Data Lake. 

Data is saved in the Data Lake straight away as a delta table using the `deltalake` library. We are performing here both full truncate and load, and incremental load.
# Incremental and full load
In full truncate and load we are truncating the entire target table in Data Lake and loading into it the entire data from the source table in the SQL db.

In the incremental load:
- We are only updating the target table based on changes which happened to the source table. 
- We are using a changes table which describes what changes happened to the source table, that is which records have been modified, deleted and inserted. 
- We are using extract logs which are saved in the Data Lake and they contain information about when the last time we extracted data for each table.
# Prerequisites
Before we ran this dag we need to set up the SQL database and the Data Lake as described here - [[MS SQL - Data Lake data ingestion with Airflow project -  App prerequisites|link]].
# DAG configuration
At the beginning of the definition of the task which is executed in that DAG, we are specifying which tables we will be ingesting and providing additional information needed for incremental load. 
# Creating a container in Data Lake
This DAG creates, if it doesn't exist yet, a container with a delta table that contains extract logs.Tags: 
