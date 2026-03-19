Tags: [[_My_projects]]
#MyProjects 

# Introduction
In this project we build a platform for:
- Data ingestion
- Data storage
- Data transformation
- MLOps
	- Creating, validating and saving ML models
	- Monitoring model performance
	- Retraining

Technologies used:
- Kubernetes
- Terraform
- Airflow
- Python
- dbt
- MLflow
# Dev and prod repositories
This project consists of two repositories:
- Dev - [data_and_ml_platform_kind](https://github.com/bulka4/data_and_ml_platform_kind) 
- Prod - [data_and_ml_platform](https://github.com/bulka4/data_and_ml_platform) 

The dev repository is used for running the platform on kind (Kubernetes in Docker), a local Kubernetes cluster running on localhost.

The prod repository is used for running the platform on AKS (Azure Kubernetes Service) and using other cloud services.
# Infrastructure
Below sections and documents describe infrastructure setup, that is how do we set up all the tools which we then can use for developing applications.
## Infrastructure guide
A guide for how to set up infrastructure:
	 - [[Data and ML platform project - Prod repository guide (AKS)]]
	 - [[Data and ML platform - Dev repository guide - kind setup]]
## Cloud resources
Below document explains:
- What cloud resources we set up
- How do we configure them
- How do we use Terraform for that
[[Data and ML platform project - Cloud resources]] 
## kind cluster for local testing
Below document describes setting up a kind Kubernetes cluster for local testing before deploying on AKS:
[[Data and ML platform - Setting up a kind cluster]] 
## Docker image for interacting with AKS
This document describes the Docker image which can be used for interacting with AKS and other cloud resources: [[Data and ML platform project - Docker image for interacting with Kubernetes]]

In that container we have prepared all the tools needed, like for example `kubectl`.
## Platform components (to delete)
This document gives overview of all the components of this platform, like cloud resources, Kubernetes resources, applications we run - [[Data and ML platform project - Components]].
## Code development
Those documents describe how to set up environment for developing code on Kubernetes:
- Using VS Code Kubernetes extension for this project - [[Data and ML platform project - VS Code Kubernetes extension setup for code development|link]] 
- Code development on Kubernetes general notes - [[Data and ML platform project - Code development setup|link]] 
## Making code available in pods
This document describes how do we make code available in pods, i.e. either via git-sync or by cloning a git repo in an init container - [[Data and ML platform project - Making code available in pods]].
## Data storage
This document describes data storage systems used for this platform - [[Data and ML platform project - Data storage]]
## Airflow setup
Those documents describe how do we setup Airflow:
- [[Data and ML platform project - Airflow setup (prod, AKS)]]
- [[Data and ML platform project - Airflow setup (dev, kind)]]
## Data transformation setup
Below sections describe how to set up tools used for data transformation:
- Spark Thrift Server with Iceberg
- dbt
- Hive Metastore (optional, not used currently)
### Spark Thrift Server and Iceberg
Those documents explain how do we set up Spark Thrift Server and Iceberg:
- [[Data and ML platform project - Spark Thrift Server setup]]
- [[Data and ML platform project - Spark Thrift Server setup - Details]]
### dbt
This document explains how do we set up dbt - [[Data and ML platform project - dbt setup]]
### Hive Metastore
This document explains how do we set up Hive Metastore - [[Data and ML platform project - Hive Metastore setup]]

Using Hive Metastore is optional, we don't use it currently.
## MLflow setup
We use MLflow for ML model creation, monitoring and retraining.

More details can be found here - [[Data and ML platform project - MLflow setup]].
# Data and ML workflows
Below sections and documents describe how to use this platform to create data and ML workflows.
## Platform usage guide
A guide for how to use this platform for data processing and developing ML models:
- [[Data and ML platform project - Using the platform guide]]
## Code development & testing scripts
This document explains how we can develop code on a local computer and run it on Kubernetes to test it - [[Data and ML platform project - Code development & testing scripts]]
## Common code
In the `apps/common` folder we have a common code used by all other applications.
## Workflow orchestration with Airflow
This document describes how workflow orchestration looks like - [[Data and ML platform project - Workflow orchestration with Airflow]].
## Data transformation
Documents about data transformation:
- [[Data and ML platform project - Data transformation workflow (dev, kind)]]
	- [[Data and ML platform project - dbt with Airflow]]
## Data ingestion
This document describes how do we perform data ingestion - [[Data and ML platform project - Data ingestion]]
## MLOps with MLflow
MLOps consists of:
- ML model creation
- Performance monitoring
- Retraining
- Updating the model used in production with a new one

More info about this workflow using MLflow on this platform can be found in documents below:
- [[Data and ML platform project - MLOps with MLflow]]
	- [[Data and ML platform project - Making and saving predictions]]
	- [[Data and ML platform project - MLOps - MLflow workflow]]
	- [[Data and ML platform project - Code - MLflow projects]]
	- [[Data and ML platform project - Code development & testing scripts]]
# Code
## MLflow projects
Notes about MLflow code - [[Data and ML platform project - Code - MLflow projects]]
# Optional improvements for later
## Monitoring
Use Prometheus and Grafana for monitoring.
## Jupyter Notebook
Set up a server running a Jupyter Notebook which users can use over a browser to use Spark.
## Training with DeepSpeed
Training models using DeepSpeed and Kubeflow TrainingRuntime CRD like described here - [[DeepSpeed cluster project]].
## RAG system
RAG system with access to dbt data dictionary. Use the RAG system I already created and modify it - [[RAG app project]].
## PyIceberg
Use PyIceberg for writing data into the Iceberg catalog instead of Spark. That can be used for example when:
- Ingesting data from external sources
- Making prediction with a ML model and saving them in an Iceberg table

Benefit of that is that PyIceberg image would be much smaller than the Spark one and we don't need to mount Spark configuration files.
# Reference docs
Official docs which describes tools used in this project are listed here - [[Data and ML platform project - Official docs]]
# To do next
Notes about what to do next - [[Data and ML platform project - To do]] 
# Questions
- Is the `as_of_date` a tag assigned to a table by dbt to know when it was created?
- 