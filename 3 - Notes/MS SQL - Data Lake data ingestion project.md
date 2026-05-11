Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Here is a Python code which is ingesting data from a MS SQL database into the Azure Data Lake. We are performing here both full truncate and load, and incremental load.

Code from this project is used in another project where we orchestrate data ingestion process using Airflow - [[MS SQL - Data Lake data ingestion with Airflow project]].

In this repository we are using the Delta Lake framework for storing data as delta tables in Azure Data Lake. We are using the deltalake library ([delta-io.github.io/delta-rs](https://delta-io.github.io/delta-rs/)). Don't confuse it with the delta library ([docs.delta.io/0.4.0/api/python](https://docs.delta.io/0.4.0/api/python/index.html#), [docs.delta.io/latest](https://docs.delta.io/latest/index.html)). Delta library requires to use Spark engine, deltalake doesn't.
# Code repository
Repository with the code: [github.com](https://github.com/bulka4/data_lake_data_ingestion) 
# Repository guide
Guide about how to use code from this repository - [[MS SQL - Data Lake data ingestion project - Repository guide|link]].
# Prerequisites
Prerequisites we need to satisfy before we start using code from this project - [[MS SQL - Data Lake data ingestion project - Prerequisites|link]].
# Code explanation
- Full and truncate load explanation - [[MS SQL - Data Lake data ingestion project - Full and truncate load explanation|link]] 
- Script configuration - [[MS SQL - Data Lake data ingestion project - Script configuration|link]] 
- SQL db data ingestion - [[MS SQL - Data Lake data ingestion project - SQL db data preparation|link]] 
- Data Lake data ingestion - [[MS SQL - Data Lake data ingestion project - Data Lake data ingestion|link]] 
- Data Lake cleanup - [[MS SQL - Data Lake data ingestion project - Data Lake cleanup|link]] 
- Classes - [[MS SQL - Data Lake data ingestion project - Classes|link]] 