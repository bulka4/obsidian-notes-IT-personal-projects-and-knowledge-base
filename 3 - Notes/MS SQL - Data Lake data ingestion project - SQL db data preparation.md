Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We are ingesting manually created data into SQL which will be then ingested by the script into Data Lake.

We use for that `sql_ingestion_v1.py` and `sql_ingestion_v2.py` scripts. 

At the beginning of those scripts we are defining what records are gonna be ingested into which tables. 

Into the changes table 'table2_changes' we are ingesting the current date into the column indicating when that record was created (that is when the change happened to the source table 'table2').