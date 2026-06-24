Tags: [[__My_projects]]
#MyProjects 

# Introduction
Below sections and documents describe infrastructure setup, that is how we set up all the tools which we then can use for developing applications.
# Accessing services UIs
We can access UIs of different services by using below URLs in a browser:
- Airflow UI - `localhost:8080`
- MLflow Tracking server UI - `localhost:5000`
- Grafana - `localhost:3000`
# Cloud resources
Below document explains:
- What cloud resources we set up
- How we configure them
- How we use Terraform for that

for both development on kind and production on AKS:
- [[Data and ML platform project - Cloud resources - Prod]]
- [[Data and ML platform project - Cloud resources - Dev]]
# Preparing files with Terraform
Terraform code except for creating cloud resources, it also prepares files on the localhost with proper values about created cloud resources.

More info can be found here - [[Data and ML platform project - Preparing files with Terraform]].
# kind cluster for local testing
Below document describes setting up a kind Kubernetes cluster for local testing before deploying on AKS:
[[Data and ML platform - Setting up a kind cluster]] 
# Docker image for interacting with Kubernetes
We can use a Docker image for interacting with:
- kind
- AKS 
- Other cloud resources

Below documents describes how this image works for both dev and prod:
- Prod - [[Data and ML platform project - Docker image for interacting with AKS]]
- Dev - [[Data and ML platform project - Docker image for interacting with kind]]

In that container we have prepared all the tools needed, like for example `kubectl`, Helm or Azure CLI.
# Code development & testing scripts
Those documents explain how we can develop code on a local computer and run it on Kubernetes to test it:
- [[Data and ML platform project - Code development & testing scripts]]
	- [[Data and ML platform project - VS Code Kubernetes extension setup for code development]]
	- [[Kubernetes - Code development]]
# Making code available in pods
This document describes how we make code available in pods, i.e. either via git-sync or by cloning a git repo in an init container - [[Data and ML platform project - Making code available in pods]].
# Data storage
Those documents describe data storage systems used for this platform:
- [[Data and ML platform project - Data storage]]
- [[Data and ML platform project - Iceberg storage framework setup]]
# Airflow setup
Those documents describe how we setup Airflow:
- [[Data and ML platform project - Airflow setup (prod, AKS)]]
- [[Data and ML platform project - Airflow setup (dev, kind)]]
# Data transformation setup
Below sections describe how to set up tools used for data transformation:
- Spark Thrift Server with Iceberg
- dbt
- Hive Metastore (optional, not used currently)
## Spark Thrift Server and Iceberg
Those documents explain how we set up Spark Thrift Server and Iceberg:
- [[Data and ML platform project - Spark Thrift Server setup]]
- [[Data and ML platform project - Spark Thrift Server setup - Details]]
## dbt
This document explains how we set up dbt - [[Data and ML platform project - dbt setup]]
## Hive Metastore
This document explains how we set up Hive Metastore - [[Data and ML platform project - Hive Metastore setup]]

Using Hive Metastore is optional, we don't use it currently but the code is prepared and it worked.
### Hive vs Iceberg
We can could use:
- Only Hive Metastore
- Both Hive Metastore and Iceberg together

Hive can be used like Iceberg to manage metadata allowing Spark to execute SQL queries.

More info about comparison between Hive and Iceberg can be found here - [[Iceberg vs Hive]].
# MLflow setup
We use MLflow for ML model creation, monitoring and retraining.

More details about setting it up can be found here - [[Data and ML platform project - MLflow setup]].
# Spark Operator
This document explains how to set up Spark Operator - [[Data and ML platform project - Spark Operator setup]]
# Prometheus
This document explains how to set up Prometheus - [[Data and ML platform project - Prometheus setup]]