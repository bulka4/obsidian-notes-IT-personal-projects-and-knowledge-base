Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
- Terraform installation and basic tutorial: [developer.hashicorp.com](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/infrastructure-as-code)
- When Terraform is creating Azure resources it is authenticating using a Service Principal. In order to allow Terraform to create other Service Principals, we need to create a Service Principal with proper permissions which will be used by Terraform for authentication.

In the ‘Authenticate using the Azure CLI > Create a Service Principal’ section in the instruction on developer.hashicorp.com we are creating a service principal with the ‘Contributor’ Azure role and we need to change it into ‘Owner’.

Also it is useful to add some name to the created service principal, for example ‘Terraform’. We can do this by using the ‘az ad sp create-for-rbac’ command with the ‘--name’ parameter.

Additionaly we need to assign the ‘Application Administrator’ Entra role to that service principal. It is described here how to do this: [docs.azure.cn](https://docs.azure.cn/en-us/entra/identity/role-based-access-control/manage-roles-portal?tabs=admin-center)

#Cloud #DevOps #InfrastructureEngineering #Terraform 