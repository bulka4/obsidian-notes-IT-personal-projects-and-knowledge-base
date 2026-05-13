Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We can divide the process of deploying the MLflow Tracking Server into two parts:
- MLflow Tracking Server - Initial preparations
- Deploy the MLflow Tracking Server as a Deployment

We will also deploy a Service for the Tracking Server's Deployment.

Below are more details about this process. All the steps described here are performed by bash scripts executed on the VM1 by Terraform.
# MLflow Tracking Server - Initial preparations
Before we can deploy the MLflow Tracking Server's Deployment, we need to prepare the main components of the Tracking Server ([[MLflow on Kubernetes on Linux VMs project - Tracking Server architecture|link]]):
- Using a bash script that Terraform runs on a VM ([[MLflow on Kubernetes on Linux VMs project - Configuring VMs using bash scripts|link]]):
	- Docker Image for MLflow Tracking Server
- Using the `/home/azureadmin/k8s/mlflow_deploy.sh` script:
	- Kubernetes namespace
	- MySQL with a volume
	- Secrets
		- Azure Storage Account connection string
		- MySQL URI (including a password)
		- Secret for accessing ACR (to pull Docker image for Tracking Server)
# Deploy the MLflow Tracking Server as a Deployment
After those preparations we can deploy the Tracking Server Deployment:
- We run the `mlflow server` command in a Pod with proper arguments
- We create a Service for it to assign a DNS name to it