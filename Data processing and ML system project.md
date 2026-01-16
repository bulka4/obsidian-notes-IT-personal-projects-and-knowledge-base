Tags: [[_My_projects]]
#MyProjects 

# Introduction
This is a system for:
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
# Data storage
For data storage we use Azure Data Lake and Delta Lake storage layer.
# Data ingestion
Data ingestion is performed using Python. Python script is ran in a pod on any Kubernetes node which has available resources.

We use KubernetesPodOperator to create a pod from Airflow.
# Data transformation
For data transformation we use dbt and Spark. There are two options for tools which we can use to run Spark:
- Spark Operator
- Thrift Server

Most probably the Thrift Server is the best option.

More information about it can be found here - [[Data processing and ML system project - Data transformation]].

