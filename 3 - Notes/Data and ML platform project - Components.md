Tags: [[_My_projects]]
#MyProjects 

# ACR
- We use ACR for storing Docker images which we use to run applications on Kubernetes
- It is created using Terraform
# Service Principal
Terraform creates a Service Principal with permissions for:
- Pulling and pushing images from ACR (for deploying pods on Kubernetes)
- Getting credentials to AKS (creating .kube/config file) so we can interact with AKS using `kubectl` CLI tool
- Saving and reading data from Azure Storage Account

It is used by many parts of the platform:
- Airflow to save logs in Azure Storage Account
- Spark to read and save data in Azure Storage Account
- When deploying all the pods (Spark Thrift Server, Hive Metastore, MLflow, Airflow etc) it is used when pulling images from ACR
# Storage Account
We use Azure Storage Account (object storage) for storing:
- DWH (data warehouse) data 
	- Used for analytics and ML
	- We use Delta Lake storage framework for that data
- Airflow logs
- MLflow artifacts

We have the following Storage Accounts and containers:
- dwhbulka Storage Account
	- DWH container
		- DWH (data warehouse) data
	- mlflow container
		- MLflow artifacts
- systemfilesbulka Storage Account
	- airflow-logs container
		- Airflow logs
# Kubernetes resources
## Secrets
We create secrets for storing credentials for accessing different systems from pods:
- ACR
- Storage Account