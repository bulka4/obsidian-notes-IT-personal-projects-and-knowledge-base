Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In the common/classes folder we are specifying all the classes which will be used by all the DAGs. We have the following classes defined:
## `AzureBlob`
This is a class for working with containers, directories and files (creating them, deleting, renaming). This class is a parent to the DeltaLake and ExtractLogs classes.
## `DeltaLake`
This is a class for working with delta tables (creating, writing data, reading data, updating them incrementally). It extends the AzureBlob class.
## `SQL`
This is a class for working with SQL. This class is used in the DataIngestion class.
## `ExtractLog`
This is a class for working with extract logs which are used for incremental load. This class is a parent to the DataIngestion class.
## `DataIngestion`
This is a class for creating data ingestion pipelines. There are functions for full and incremental load.