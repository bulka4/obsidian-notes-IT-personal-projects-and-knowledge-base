Tags: [[__My_projects]] [[__Machine_Learning_Engineering]]
#MyProjects #MLEngineering 

# Infrastructure
Infrastructure is prepared using Terraform and Helm:
- Terraform creates AKS and all the other cloud resources (in Azure) needed
- Using Helm we deploy a MLflow Tracking server and run a MLflow project

We also:
- Prepare a Docker image which can be used to interact with Kubernetes ([[MLflow on AKS project - Docker container for interacting with AKS|link]]). It contains all the tools to do so (e.g. Helm and `kubectl` installed).
- Mount Azure File share to a pod running a MLflow project
	- So we can upload there files with code to run
# Project architecture
The main components of this solution are:
- MLflow Tracking server
	- Responsible for saving workflow’s metadata and artifacts
- MySQL 
	- Acts as a backend store
- MLflow project
	- Defines what scripts to run in our ML workflow
- Azure Storage Account 
	- Acts as an artifact store
