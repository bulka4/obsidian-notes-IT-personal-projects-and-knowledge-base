Tags: [[_My_projects]]
#MyProjects 

# Introduction
We orchestrate workflow using Airflow. That workflow includes:
- Data transformations using dbt
- Making predictions using a model from MLflow registry and saving them in the Iceberg catalog using Spark
# Testing Airflow code
For testing Airflow code, for example custom operators from `airflow/dags/common` folder or creating pods using Kubernetes Python client, we can use the `helm_charts/development_pods/airflow` Helm chart which prepares a development pod ([[Data and ML platform project - Code development & testing scripts|link]])
# Running Kubernetes jobs
We run Airflow tasks as Kubernetes jobs because jobs can restart in case of failure. We create those Airflow tasks such that:
- Task finishes when the job finishes
- Wen job fails, then Airflow task fails as well
# dbt with Airflow
Notes about using dbt with Airflow are here - [[Data and ML platform project - dbt with Airflow]].
# Making and saving predictions
More info about making and saving predictions - [[Data and ML platform project - Making and saving predictions]].

Info about how to run it with Airflow - [[Data and ML platform project - Making and saving predictions - Airflow orchestration]]
# Automatic update of ML models based on their performance
More info about Airflow DAG for automatic update of ML models - [[Data and ML platform project - Automatic update of ML models based on their performance]].