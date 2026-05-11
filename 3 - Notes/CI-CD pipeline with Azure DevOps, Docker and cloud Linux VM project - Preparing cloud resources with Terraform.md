Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
Terraform code is in the `terraform` folder and it creates:
- **ACR** - For storing Docker images which we will be deploying
- **Service Principal** - For authentication when pushing and pulling images from ACR
- **Azure Linux VM** - Where we will be running a Docker container and a Self Hosted Agent

And additionally:
- **Executes a bash script on the created VM** - Which will install:
    - **Docker** - Needed for running app as a container
    - **Azure Pipelines Self Hosted Agent** - Needed to perform actions from our defined CI/CD pipeline
- **Generates SSH keys pair** - Which we can use for connecting to the created VM.
# Prerequisites before we run Terraform code
Before we run this Terraform code we need:
- An Agent Pool prepared
- In that Pool there can't be any Agent with the same name as the new Agent we want to create

Otherwise, executing a bash script on this VM will fail.
# The `modules` folder
That folder contains Terraform modules where each module is creating different Azure resources.
# Terraform outputs
Terraform generates outputs we can access and which we will need as described here - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Terraform outputs|link]].
# SSH key generation
Terraform generates SSH keys which we can use to connect to the created VM - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - SSH key generation|link]].
# VM configuration with a bash script
Terraform executes a bash script on the created VM to configure it as described here - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - VM configuration with a bash script|link]].