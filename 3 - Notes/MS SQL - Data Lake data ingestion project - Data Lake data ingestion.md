Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
The `data_lake_ingestion.py` script is ingesting data from SQL db into the Data Lake. Before we do that we need to at first prepare data into that SQL db like described here - [[MS SQL - Data Lake data ingestion project - SQL db data preparation|link]].

That script creates:
- The `source-data` container in that Data Lake with the `source_data` folder 
	- It will contain data ingested from the SQL db. 
- Creates the `extract-logs` container with the `extract_logs` delta table 
	- It will contain extract logs with information about when the last time we were extracting data for each table what is needed for incremental load. 

We use here the following classes ([[MS SQL - Data Lake data ingestion project - Classes|link]]):
- `AzureBlob` - For creating containers and folders
- `ExtractLog` - For working with extract logs
# Script configuration
At the beginning of that script we need to provide information about:
- From which tables we will be ingesting data and provide additional information needed to perform an incremental load.
- Name of the container and directory which we will create and where we will be ingesting data.