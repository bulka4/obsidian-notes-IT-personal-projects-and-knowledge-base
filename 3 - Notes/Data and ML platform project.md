Tags: [[__My_projects]]
#MyProjects 

# Introduction
In this project we build a platform that can be deployed on Kubernetes and used for:
- **Data ingestion** - Using Python scripts
- **Data storage** - Using Azure Data Lake Gen2 (object data storage) and Iceberg
- **Distributed data transformation** - Using Spark and dbt
- **MLOps** - Using MLflow:
	- Training, evaluating and registering ML models
	- Experiment tracking (keeping track of information about models we create, e.g. hyperparameters used or evaluation metrics)
	- Automatic model update when its performance drops
- **Workflow orchestration** - Using Airflow

As a part of this project, we also build an example ML pipeline (data pipeline + CI/CD for ML) using this platform.

Technologies used:
- **Docker and Kubernetes** - Containers and orchestration
- **Terraform** - IaC
- **Airflow** - Workflow orchestration
- **dbt and Spark** - Data transformation
- **Iceberg and Azure Data Lake Gen2** - Object data storage and table format enabling running SQL queries
- **MLflow** - MLOps
- **Python, SQL, bash** - Programming languages
# Platform overview
Here is a high level overview of the most important features of this platform - [[Data and ML platform project - Platform overview]].
# Benefits
High level overview of benefits of using this platform - [[Data and ML platform project - Benefits]].
## Benefits of the tools used
More detailed benefits of individual tools used in this platform:
- Airflow - [[Data and ML platform project - Airflow - Benefits and key features]]
- dbt - [[Data and ML platform project - dbt benefits]]
- Spark enables partitioning data what has benefits described here - [[Data Engineering - Partition-based writes]].
- Spark Operator - [[Spark Operator - Pros and cons]]
- Iceberg - [[Iceberg - Benefits]]
	- Hive vs Iceberg comparison - [[Iceberg vs Hive]]
- MLflow - [[Data and ML platform project - MLflow - Benefits and key features]]
# Dev and prod repositories
This project consists of two repositories:
- Dev - [data_and_ml_platform_kind](https://github.com/bulka4/data_and_ml_platform_kind) 
- Prod - [data_and_ml_platform](https://github.com/bulka4/data_and_ml_platform) 

The dev repository is used for running the platform on kind, a Kubernetes cluster running in Docker on localhost.

The prod repository is used for running the platform in cloud on AKS (Azure Kubernetes Service).
## Code status
The dev repository contains all the features. The prod one, only a part of them.
# Infrastructure guide
A guide for how to set up infrastructure:
 - [[Data and ML platform project - Prod repository guide (AKS)]]
 - [[Data and ML platform - Dev repository guide - kind setup]]
# Example workflow
An example workflow created on this platform for data processing and developing ML models - [[Data and ML platform project - Example workflow|link]].
# Infrastructure
How infrastructure was prepared for this platform and how it works (configuring all the tools, deploying on Kubernetes, accessing services through a browser) - [[Data and ML platform project - Infrastructure|link]].
# Data and ML workflows
How to build workflows on this platform - [[Data and ML platform project - Data and ML workflows|link]].
# Code
- MLflow projects - [[Data and ML platform project - MLflow projects code|link]] 
# Problems encountered during the project
What problems we encountered during working on this project - [[Data and ML platform project - Problems encountered during the project|link]].
# Optional improvements for later
Optional improvements for this project for later - [[Data and ML platform project - Improvements for later|link]].
# Reference docs for the tools used
Official docs which describe tools used in this project are listed here - [[Data and ML platform project - Official docs for the tools used|link]].
# To do next
Notes about what to do next - [[Data and ML platform project - To do]] 