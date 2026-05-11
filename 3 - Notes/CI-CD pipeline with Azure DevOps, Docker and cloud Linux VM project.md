Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
This repository contains code for preparing infrastructure for creating a CI/CD pipeline using Azure Pipelines which deploys an application as a Docker container on Azure Linux VM.

Code from this repo doesn't build the CI/CD pipeline itself. It only prepares all the resources needed and after that we can create a CI/CD pipeline on Azure DevOps website with a minimal manual effort. 

Using infrastructure prepared by this code we can create a CI/CD pipeline deploying for example Airflow app from the `airflow_data_lake_ingestion` repository ([github.com](https://github.com/bulka4/airflow_data_lake_ingestion)).
# Code repository
Repository with project's code - [github.com](https://github.com/bulka4/azure_ci_cd).
# Pipeline design
[[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Pipeline design]]
# Repository guide
[[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Repository guide]]
# Prerequisites
[[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Prerequisites]]
# Preparing cloud resources with Terraform
- Preparing cloud resources - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Preparing cloud resources with Terraform|link]] 
- Terraform outputs - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Terraform outputs|link]] 
- Generating SSH keys - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - SSH key generation|link]] 
- VM configuration - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - VM configuration with a bash script|link]] 
# Preparing Azure DevOps resources
- DevOps Rest API code - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Creating DevOps resources using Rest API|link]] 
- Create an Agent Pool - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Create an Agent Pool|link]] 
- Add Service Principal credentials to the Variable group in DevOps Library - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Add Service Principal credentials to the Variable group|link]] 
- Create a Service connection in DevOps linked to the ACR  - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Create a Service connection in DevOps linked to the ACR|link]] 
- Generate a YAML file - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Generate a YAML file|link]] 
# Dockerfile and docker-compose preparation
How to prepare `Dockerfile` and `docker-compose.yml` files - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Dockerfile and docker-compose preparation|link]].
# Code issues
Code issues - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Code issues|link]].
