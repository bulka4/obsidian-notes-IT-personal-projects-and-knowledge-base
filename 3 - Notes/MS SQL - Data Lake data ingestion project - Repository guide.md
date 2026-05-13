Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We can use those scripts in order to simulate an incremental load from a MS SQL db into a Azure Data Lake. In order to do that we need to follow the below steps. All those steps and scripts used in them are described below in this document in the sections 'SQL db data ingestion' and 'Data Lake data ingestion'.
- **SQL db data ingestion part 1** - First we are preparing initial data in the SQL db which will be later on ingested into the Data Lake. We do this using the sql_ingestion_v1.py script. We are preparing here 3 tables:
    - db.fact.table1 - data from this table will be ingested into the Data Lake using a full truncate and load.
    - db.fact.table2 - data from this table will be ingested into the Data Lake using an incremental load.
    - db.fact.table2_changes - changes table describing what changes happened to the 'table2' table. It will be used for an incremental load.
- **Data Lake setup** - After that we need to create a container and directory in that container where we will be ingesting data. For that we are using the data_lake_setup.py script which is using Azure SDK.
- **Data Lake data ingestion part 1** - Then we can ingest data from SQL db which we prepared in the previous step into the Data Lake. We do this using the data_lake_ingestion.py script. We are performing full truncate and load for db.fact.table1 and incremental load for db.fact.table2
- **SQL db data ingestion part 2** - As the third step we are making changes in the 'table2' and 'table2_changes' tables in the SQL db:
    - We are ingesting one additional record into the 'table2' table.
    - We are modifying one record into the 'table2' table.
    - We are deleting one record into the 'table2' table.
    - We save information about those changes in the table2_changes table.
    We make those changes in order to test if incremental load is working properly. We perform this step using the sql_ingestion_v2.py script.
- **Data Lake data ingestion part 2** - In the end we are performing again data ingestion into the Data Lake in order to test incremental load. We should add one record to the target table, modify one and delete one. We do this using again the data_lake_ingestion.py script.