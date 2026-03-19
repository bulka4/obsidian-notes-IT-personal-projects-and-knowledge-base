Tags: [[_My_projects]]
#MyProjects 

# Introduction
We use Azure Storage Account (object storage) for storing:
- DWH (data warehouse) data 
	- Used for analytics and ML
	- We use Delta Lake storage framework for that data
- Airflow logs
- MLflow artifacts

Additionally, we use:
- PostgreSQL for Hive Metastore metadata (deployed on Kubernetes)
- PostgreSQL for Airflow metadata (deployed on Kubernetes)
- MySQL as a MLflow backend store (deployed on Kubernetes)