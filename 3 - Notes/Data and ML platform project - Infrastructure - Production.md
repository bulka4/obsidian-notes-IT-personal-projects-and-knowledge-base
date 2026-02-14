Tags: [[_My_projects]]
#MyProjects 

# Introduction
Terraform prepares:
- Azure Data Lake
- AKS
- ACR
- Service Principal
- Files saved on the localhost:
	- Dockerfile for creating an image for interacting with AKS
	- values.yaml files for Helm charts

More information about objects prepared by Terraform can be found here - [[Data and ML platform project - Components]].
# VNet
We don't create here a VNet so we can easily access AKS from our local computer. For production, it is recommended to use an VNet for security as explained here - [[Azure VNet]].
# Preparing files
Terraform prepares the following files and saves them on the localhost:
- `values.yaml` for Helm charts:
	- `helm_charts/airflow/values.yaml`
	- `helm_charts/mlflow_project/values.yaml`
	- `helm_charts/mlflow_setup/values.yaml`
	- `helm_charts/spark_thrift_server/values.yaml`
- Dockerfile for building an image for interacting with AKS:
	- `interacting.aks.Dockerfile`

Templates of those files are in the `terraform/teplate_files` folder and Terraform interpolates them (inserts into them values of variables).