Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
This is an Airflow app with a DAG for ingesting data incrementally from a MySQL database into a Delta Lake tables in Azure Data Lake Gen2.

It is containerized using Docker. It can be ran on a local computer using Docker or it can be deployed on Azure Linux VM using Azure Pipelines and the `azure-pipelines.yml` YAML file.

This project uses functions from another project as well - [[MS SQL - Data Lake data ingestion project]] which are used for:
- Initial setup to test the ingestion, i.e. preparing sample data in MS SQL database and container in Azure Data Lake.

**Implementation:**
Testing this data ingestion process can be done in the following way:
- Run Terraform code to create MS SQL database and Azure Data Lake which we will be used in data transfer
- Run the script that prepares sample data in MS SQL database
- Run the script that sets up a container in Azure Data Lake where data will be ingested
- Run Airflow application using Docker Compose 
- Trigger the data ingestion process from Airflow website

**Delta Lake table format**
We use the Delta Lake table format for storing data in Azure Data Lake. 

We use the deltalake library ([delta-io.github.io/delta-rs](https://delta-io.github.io/delta-rs/)). Don't confuse it with the delta library ([docs.delta.io/0.4.0/api/python](https://docs.delta.io/0.4.0/api/python/index.html#), [docs.delta.io/latest](https://docs.delta.io/latest/index.html)). 

Delta library requires to use Spark engine, deltalake doesn't.
# PowerPoint presentation and videos
Additional PowerPoint presentation and videos are in my Google Drive - [drive.google.com](https://drive.google.com/drive/u/0/folders/1LOh4xlQR1iAQDKS7_v0EkziSC0kgOYCL).
# Code repositories
Repositories with the code:
- Airflow app - [airflow_data_lake_ingestion](https://github.com/bulka4/airflow_data_lake_ingestion) 
- Repository with functions we will be using in this project as well - [data_lake_data_ingestion](https://github.com/bulka4/data_lake_data_ingestion) 
- Terraform code for creating the Azure MS SQL db and Azure Data Lake - [azure_terraform](https://github.com/bulka4/azure_terraform) 
- Code for creating a CI/CD pipeline for deploying this app - [azure_ci_cd](https://github.com/bulka4/azure_ci_cd) 
# Running the app
In order to start the Ariflow on our local computer we need to run this command to run Docker containers:
```
docker compose up
``` 
# App prerequisites
Prerequisites that we need to satisfy before using this app - [[MS SQL - Data Lake data ingestion with Airflow project -  App prerequisites|link]].
# App's code notes
- Python classes we use - [[MS SQL - Data Lake data ingestion with Airflow project - Python classes|link]] 
- Python libraries required for DAGs - [[MS SQL - Data Lake data ingestion with Airflow project - Python libraries required for DAGs|link]] 
- DAG for data ingestion - [[MS SQL - Data Lake data ingestion with Airflow project - DAGs|link]].
# Ideas for improvements
Ideas for the future improvements of this application - [[MS SQL - Data Lake data ingestion with Airflow project - Ideas for improvements|link]].
# Docker notes
Important aspects of how to use Docker for running this app - [[MS SQL - Data Lake data ingestion with Airflow project - Docker|link]].
# App deployment
How to create a CI/CD pipeline in Azure DevOps which will run this app on Azure Linux VM in a Docker container - [[MS SQL - Data Lake data ingestion with Airflow project - CI - CD pipeline for app deployment|link]].