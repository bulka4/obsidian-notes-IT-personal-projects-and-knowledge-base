Tags: [[__My_projects]]
#MyProjects 

# Introduction
Metadata extraction is a data pipeline extracting and saving SQL database metadata:
- Tables and columns
- Scripts (from views, jobs, stored procedures)

This metadata is used to generate data lineage graphs and create a list of tables and columns for which users can create documentation.

This pipeline is:
- programmed in Python
- scheduled using a CronJob