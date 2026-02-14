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
# Repository guide
Information about how to use code from both prod and dev repositories is here:
 - [[Data and ML platform project - Prod repository guide (AKS)]]
 - [[Data and ML platform - Dev repository guide (kind)]]
# Infrastructure
## Prod
For preparing infrastructure to run our platform in production we use:
- AKS - Kubernetes cluster to run applications on
- ACR - Container registry where we keep Docker images used to run applications on Kubernetes
- Terraform - IaC (infrastructure as code) tool for preparing Azure resources

More details about it can be found here: [[Data and ML platform project - Infrastructure - Production]]
## Dev
How we are preparing a kind cluster for development is described here - [[Data and ML platform - Setting up a kind cluster]].
# Docker image for interacting with AKS
Terraform creates a Dockerfile which can be used to build an image from which we can interact with AKS and ACR through CLI using:
- Helm
- kubectl
- Azure CLI

From inside of that image we perform operations like:
- Building Docker images and pushing them to ACR
- Deploying Helm charts
- Interacting with Kubernetes pods (checking statuses, logs, connecting to them and executing CLI commands)

More details about it can be found here - [[Data and ML platform project - Docker image for interacting with AKS]]
# Platform components
Components from which this platform consist of:
- AKS (Kubernetes cluster) for running applications
- Azure Service Principal for authentication when accessing different Azure services
- MLflow Tracking Server
- and more
are described here - [[Data and ML platform project - Components]]
# Data storage
We use Azure Storage Account (object storage) for storing:
- DWH (data warehouse) data 
	- Used for analytics and ML
	- We use Delta Lake storage framework for that data
- Airflow logs
- MLflow artifacts

Additionally, we use:
- PostgreSQL for Hive Metastore metadata (deployed on AKS)
- PostgreSQL for Airflow metadata (deployed on AKS)
- MySQL as a MLflow backend store (deployed on AKS)
# Workflow orchestration with Airflow
All the processes are orchestrated using Airflow:
- Data ingestion
- Data transformation
- Running MLflow projects

- We use git-sync to pull code from a repo, with Airflow tasks to run, into Kubernetes pods where code will be executed 
- Airflow logs (which are also visible in Airflow UI) are being saved in an Azure Storage Account
- We use PostgreSQL as Airflow's metadata db (deployed on Kubernetes as well)

More information can be found here:
- [[Data and ML platform project - Workflow orchestration with Airflow (prod, AKS)]]
- [[Data and ML platform project - Workflow orchestration with Airflow (dev, kind)]]
# Data ingestion
Data ingestion is performed using Python. Python script is ran in its own pod on Kubernetes created by the Airflow KubernetesPodOperator.
# Data transformation
For data transformation we use dbt and Spark. For running Spark we use Thrift Server.

More information about it can be found here
- [[Data and ML platform project - Data transformation (prod, AKS)]]
- [[Data and ML platform project - Data transformation (dev, kind)]]
## Different data refreshing times
Tables have different refresh time, some of them are being updated daily while others are being updated weekly or monthly.

We update all the tables with the same refresh time by using tags (we run a single dbt run command and it builds all the tables with a specific tag which corresponds to a specific refresh time).
# MLflow setup
We use MLflow for ML model creation, monitoring and retraining.

More details can be found here - [[Data and ML platform project - MLflow setup]].
# ML model creation
## Data preparation
To prepare a dataset for a model, it is probably better to prepare it together with other datasets within the same dbt run, outside of a MLflow project.

Preparing a dataset within a MLflow project might make sense only if we know, that this dataset will be used only for this one model and nothing else.
## Data reproducibility
We make sure, that when we prepare a dataset for training a model within a MLflow project, we always get exactly the same dataset, no matter when we run that project.

To ensure that, we:
- Select data within a specific time frame
- Save data used for every training in a table using Delta Lake 
	- Time travel can be used for versioning - we save different versions of data (used for different trainings) and we can access them later
- For features that change over time (like user status), use dbt snapshots
- MLflow run logs:
	- Table name or path
	- Delta version or timestamp
	- Information which tells us:
		- For which time frame we selected data for training 
		- Which version we used (For features that change over time)
	- dbt commit hash

We want to keep both:
- Data used for training (saved in a storage)
- Query which generated it

Thanks to that:
- Saved data gives us a guarantee that we will have available exactly the same dataset available which was used for training (query might not be able to reproduce it later in the future) 
- Query tells us how that dataset was created
# ML model performance monitoring
We monitor ML model performance over time as new data arrives by performing calculations described below. 

We perform those calculations using dbt whenever possible and Python for more complex calculations, and save results in tables.
## Model performance metrics
- Accuracy, RMSE etc
## Prediction behavior
Check:
- Prediction mean
- Prediction variance
- Class balance
- Confidence distribution

If those values changes significantly, something might be wrong.
## Data drift
Check for new data:
- Feature distributions
- Null rates
- Cardinality
- Summary stats

and compare it with the data used for training. If those values are different, then model can start making bad predictions.

This way we can detect problems with predictions before they appear.
# Model retraining
Once we have results of monitoring in tables, we run MLflow projects which retrains the model if specified conditions are satisfied (model performs badly).

We create many different models using different hyper parameters and datasets.
# Updating the model
Once we have new models created, then we can run a Python script which:
- Checks models' performance from MLflow database
- Picks up the best model
- Saves the model in a specified location which will be used in a production pipeline
# Optional improvements for later
## Monitoring
Use Prometheus and Grafana for monitoring.
## Jupyter Notebook
Set up a server running a Jupyter Notebook which users can use over a browser to use Spark.
## Training with DeepSpeed
Training models using DeepSpeed and Kubeflow TrainingRuntime CRD like described here - [[DeepSpeed cluster project]].
## RAG system
RAG system with access to dbt data dictionary. Use the RAG system I already created and modify it - [[RAG app project]].
# Questions
- Is the `as_of_date` a tag assigned to a table by dbt to know when it was created?
- 