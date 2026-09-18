Tags: [[__My_projects]]
#MyProjects 

# Introduction
Metadata extraction is a data pipeline extracting and saving SQL database metadata:
- Tables and columns
- Scripts (from views, jobs, stored procedures)

This metadata is used to generate data lineage graphs and create a list of tables and columns for which users can create documentation.

This pipeline is programmed in JavaScript.
# Running the pipeline
To run this pipeline:
- Deploy MS SQL Server using the `helm_charts/ms_sql` Helm chart:
	- From which we will extract metadata
  ```bash
	# Execute below commands from the helm_charts/ms_sql folder
	helm -n source-db install ms-sql . &
  ```
- Deploy MongoDB using the Helm chart:
	- We will save there extracted metadata
  ```bash
  	# Execute below commands from the helm_charts/mongo_db folder
	helm dependency build
	helm -n semantic-search install mongo-db . &
  ```
- deploy the `helm_charts/metadata_extraction` Helm chart:
  ```bash
	# Execute below commands from the helm_charts/metadata_extraction folder
	helm -n semantic-search install metadata-extraction . &
  ```
# Source SQL database
Source SQL database from which extract metadata is deployed using the `helm_charts/ms_sql` Helm chart.
# MongoDB database for metadata
Metadata extraction pipeline populates the MongoDB database with both:
- Metadata about tables, columns and scripts
- Data lineage data

It is used by the data governance backend.

More information is here:
- [[Data governance app with a RAG system - Databases - Database documentation|Database documentation]] 
- [[Data governance app with a RAG system - Databases - Data lineage data|Data lineage data]] 
# Helm chart
- We run the metadata extraction pipeline using the `helm_charts/metadata_extraction` Helm chart.
- Scripts to run are mounted into the created pod from the host.
- It uses the image built using the `dockerfiles/nodejs.Dockerfile`.
# Node.js
We use Node.js to run this pipeline, more notes about it are here - [[Data governance app with a RAG system - Tools used - Node.js]].
## npm packages
We install `npm` packages when running the pipeline. They are not baked into the Docker image to reduce its size which is already quite big and might not fit on the disk.
# Improvements
- Rewrite the code in Python, use data classes, interfaces and change responsibilities of functions. A new design for this is here - [[Data governance app with a RAG system - Metadata extraction - New code architecture|New code architecture]].
- Schedule the pipeline using a CronJob
	- It could be also scheduled in Airflow but for this project Airflow is not needed and CronJob is simpler and good enough
- Update the code such that it can update metadata (get metadata about new tables) while preserving created descriptions