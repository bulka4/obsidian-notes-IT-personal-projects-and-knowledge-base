Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
Code from the `azure_devops/ci_cd_setup` folder prepares resources in Azure DevOps needed to create a CI/CD pipeline.

This code performs the following actions:
- Create an Agent Pool - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Create an Agent Pool|link]] 
- Add Service Principal credentials to the Variable group in DevOps Library - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Add Service Principal credentials to the Variable group|link]] 
- Create a Service connection in DevOps linked to the ACR  - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Create a Service connection in DevOps linked to the ACR|link]] 
- Generate a YAML file - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Generate a YAML file|link]] 
# Folder structure
In the `azure_devops/ci_cd_setup` we have two subfolders:
- `agent_pool_setup` - Contains code for creating an Agent Pool where we will be adding a Self Hosted Agent which we will install on Azure Linux VM.
- `acr_push_and_pull` - Contains code for creating:
    - Variable group in DevOps Library
    - Service Connection in DevOps
    - YAML file

All the code from those folders uses Azure DevOps Rest API.
# Logs
There is defined a class `Logs` in the `classes > class_logs.py` file. It is used when creating and deleting resources in DevOps. It creates a folder `logs` and a file `logs.csv` containing information about which resources were created and deleted, and at what time.
# .env file configuration
As described here - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Prerequisites|link]], this code uses environment variables from the `.env` file using the `dotenv` module and `os.getenv('env_variable_name')` function.

We need to prepare this file using the `.env-draft` file.