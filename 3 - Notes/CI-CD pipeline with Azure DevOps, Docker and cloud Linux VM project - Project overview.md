Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Architecture overview
Scripts which I prepared in this project leverage Azure DevOps Rest API and Terraform allowing for:
- Creating Azure and Azure DevOps resources
- Automatic generation a YAML file which defines a CI/CD pipeline

Once those resources are prepared, CI/CD pipelines can be created this way:
- Move the generated YAML file to the repo with application want to deploy and create CI/CD pipeline on Azure DevOps website
# Guide
Creation of resources, needed to start building CI/CD pipelines, using code from this project is performed in the following way:
- Run a Python script which creates an Agent Pool in Azure DevOps using Rest API
- Run Terraform code which creates all the necessary Azure resources:
	- ACR – For storing Docker images we will be deploying
	- Service Principal - For authentication when accessing Azure resources
	- Linux VM - On which we will run our app
- Run a Python script which creates other resources in Azure DevOps (Variable group, Service connection) using Rest API and generates a YAML file which defines a CI/CD pipeline
- Move the generated YAML file to the repository of the app we want to deploy

Once this is done, it is easy to create a CI/CD pipeline on Azure DevOps website.

There are also scripts that allows for cleaning up all the resources created in Azure DevOps. Azure resources can be also easily deleted using Terraform.