Tags: [[_My_projects]]
#MyProjects 

# Kubernetes deployment
Details about how to deploy MLflow on Kubernetes like in this project, can be found here - [[MLflow - Kubernetes deployment]].
# Git-sync
We use git-sync to pull code from a repo with a MLflow project to run and mount it into a pod where that code will run.

Git-sync runs in an init container in the job running the MLflow project.
# MySQL as a backend store
We use MySQL as a backend store for MLflow Tracking Server. We deploy it using the official Helm chart, as a dependency in the Chart.yaml file.

For production it is recommended to use a managed MySQL database as running databases on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
# Azure Storage Account as an artifact store
We use an Azure Storage Account as an artifact store.
# ACR
We use an ACR for storing Docker images used to run the MLflow Tracking Server and projects in Kubernetes pods.