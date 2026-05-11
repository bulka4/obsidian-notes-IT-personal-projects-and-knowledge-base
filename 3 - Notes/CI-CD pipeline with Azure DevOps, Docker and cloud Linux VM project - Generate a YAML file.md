Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
We will generate a YAML file defining actions to perform in our CI/CD pipeline. 

This file will need to be added manually to the repo containing the code which we want to deploy onto the VM. 

It will contain an information about:
- Created Variable group in DevOps Library
- ID of the created Service connection linked to the ACR
- Name of the Agent pool to use
- Name of the ACR which will be used

Once we have the Variable group and Service connection in DevOps created, and YAML file generated, we can move this YAML file to the repository we want to deploy and create a CI/CD pipeline on DevOps website. 