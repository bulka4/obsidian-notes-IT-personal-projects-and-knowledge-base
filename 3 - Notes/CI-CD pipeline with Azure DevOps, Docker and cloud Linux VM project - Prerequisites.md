Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Azure subscription
We need to have a subscription on the Azure platform portal.azure.com.
# Terraform configuration
We need to configure properly Terraform so it can create resources in our Azure subscription, it is described here: [developer.hashicorp.com](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/azure-build).

When following this instruction, we need to perform only one step in a different way then it is described in that instruction. And that is caused by the fact that we want to allow Terraform to create Service Principals. 

When Terraform is creating Azure resources it is authenticating using a Service Principal. In order to allow Terraform to create other Service Principals, we need to create a Service Principal with proper permissions which will be used by Terraform for authentication. 

In the ‘Authenticate using the Azure CLI > Create a Service Principal’ section in the instruction on developer.hashicorp.com we are creating a service principal with the ‘Contributor’ Azure role and we need to change it into ‘Owner’.

Also it is useful to add some name to the created service principal, for example ‘Terraform’. We can do this by using the `az ad sp create-for-rbac` command with the `--name` parameter.

Additionally, we need to assign the ‘Application Administrator’ Entra role to that service principal. It is described here how to do this: [docs.azure.cn](https://docs.azure.cn/en-us/entra/identity/role-based-access-control/manage-roles-portal?tabs=admin-center)
# Terraform variables
Before using this code we need to create `terraform.tfvars` file which looks like the `terraform-draft.tfvars` file and save it in the same location. In this draft file is described what values we need to provide.

We are assigning there values to variables defined in the `variables.tf` file located in the same folder. In the `variables.tf` file we can also find descriptions and default values of those variables.

As it is written in a comment in the `terraform-draft.tfvars` file, it is necessary to provide values for just a few of variables, not all of them.
# .env file configuration
Before using this code we need to additionally create the `.env` file in two subfolders in the `azure_devops > ci_cd_setup` folder:
- `acr_push_and_pull`
- `agent_pool_setup`

In those files we need to specify values for a few environment variables which will be used in code using the `dotenv` module and `os.getenv('env_variable_name')` function. 

Those files should look like the `.env-draft` file included in those folders and they should be saved in the same location. In those files it is described what values to provide.

To provide values for some of those variables, we need to run the Terraform code first and get its outputs ([[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Terraform outputs|link]]). In those` .env-draft` files we have comments indicating which variables those are.

As it is written in a comment in the `.env-draft` file, it is necessary to provide values for just a few of variables, not all of them.
# Set up Python virtual environment
Create a virtual environment:
>`py -m venv venv`

And install all the requirements:
>`pip install requirements.txt`

Before running any Python code from the `azure_devops` folder, activate a venv:
>`venv/Scripts/activate` <- for Windows