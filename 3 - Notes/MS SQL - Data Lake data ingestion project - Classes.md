Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We have the following classes defined:
- **AzureBlob** - This is a class for working with containers, directories and files (creating them, deleting, renaming). This class is a parent to the DeltaLake and ExtractLogs classes. It is using Azure SDK.
- **DeltaLake** - This is a class for working with delta tables (creating, writing data, reading data, updating them incrementally). It extends the AzureBlob class.
- **SQL** - This is a class for working with SQL. This class is used in the DataIngestion class.
- **ExtractLog** - This is a class for working with extract logs which are used for incremental load. This class is a parent to the DataIngestion class.
- **DataIngestion** - This is a class for creating data ingestion pipelines.