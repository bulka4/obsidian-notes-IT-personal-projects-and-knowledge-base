Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In full truncate and load we are truncating the entire target table in Data Lake and loading into it the entire data from the source table in the SQL db.

In the incremental load we are only updating the target table based on changes which happened to the source table. 

For that we are using a changes table which describes what changes happened to the source table, that is which records have been modified, deleted and inserted.