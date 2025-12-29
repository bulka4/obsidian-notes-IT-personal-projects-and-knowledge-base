Tags: [[__DevOps]], [[__Infrastructure_Engineering]]

# App deployment methods

Below are different tools which we can use for deploying applications:
- Azure DevOps, Docker, Azure Container Registry, Azure Linux VM

## Azure DevOps, Docker, Azure Container Registry, Azure Linux VM

In this approach we create a CI/CD pipeline in Azure DevOps which performs the following steps:
- Take code from repository
- Build a Docker image from it
- Push that Docker image to Azure Container Registry
- Pull that Docker image onto an Azure Linux VM and run it.

![[2 - Images/App deployment/Screenshot 1.png]]

# PoCs

## Airflow app deployment - Azure DevOps, Docker, Azure Container Registry, Azure Linux VM

In this PoC I am deploying an Airflow app using Azure DevOps, Docker, Azure Container Registry and Azure Linux VM.

There is a PowerPoint presentation and videos about that in the ‘Airflow deployment - Azure DevOps, Docker, Linux VM’ folder in the same folder as this document.

Links to repositories with code used in that PoC:
- azure_devops_rest_api - [https://github.com/bulka4/azure_devops_rest_api](https://github.com/bulka4/azure_devops_rest_api)
- azure_terraform – [https://github.com/bulka4/azure_terraform](https://github.com/bulka4/azure_terraform) 
- airflow_docker - [https://github.com/bulka4/airflow_docker](https://github.com/bulka4/airflow_docker) 

# Azure DevOps

## Agent pool

Agent pool is a place where we can add Self Hosted Agents. Self Hosted Agents are installed on a computer and they perform actions defined in the CI/CD pipeline, for example push a Docker image to an Azure Container Registry or pull a Docker image onto a VM and run it.