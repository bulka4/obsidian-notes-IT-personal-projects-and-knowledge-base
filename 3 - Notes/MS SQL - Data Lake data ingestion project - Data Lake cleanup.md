Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
The data_lake_cleanup.py script deletes: 
- **Ingested data from SQL** - It deletes the source_data directory in the source-data container where we were ingesting data from SQL db.
- **Extract logs** - It deletes the extract_logs directory from the extract-logs container containing extract logs (when the last time we extracted data for each table).