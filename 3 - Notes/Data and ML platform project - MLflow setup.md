Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document explains the MLflow setup part of the Data and ML platform project. More info about that project can be found here - [[Data and ML platform project]].
# Running MLflow project
## Helm chart
We can use the `helm_charts/mlflow_project` helm chart for running a MLflow project. In `values.yaml` we specify a command to run a project, for example:
```
mlflow run https://github.com/bulka4/data_and_ml_platform_kind.git#apps/mlflow_project -e train --env-manager local --experiment-name=lasso_test
```
we specify here:
- From which repo to take the code and path to the folder with the MLflow project to run
- Which entrypoint from the MLflow project to run
- Any additional configurations for the `mlflow run` command
## Airflow
We can use Airflow to run a MLflow project. The `airflow/dags/mlflow` folder contains files for that.

The DAG file uses pod operator to run a pod using included YAML manifest which runs a MLflow project.

In that YAML manifest we specify a command to run a project, like described in the section 'Helm chart' above.
# PostgreSQL as a backend store
We use PostgreSQL as a backend store for MLflow Tracking Server. We deploy it using the official Docker image as a separate deployment in the same Helm chart.

For production it is recommended to use a managed PostgreSQL database as running databases on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
# Accessing MLflow Tracking server
We can access it through the URL: `localhost:5000`.
# Azure Storage Account as an artifact store
We use an Azure ADLS Gen2 as an artifact store.