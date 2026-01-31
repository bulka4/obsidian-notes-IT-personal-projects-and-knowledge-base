Tags: [[_My_projects]]
#MyProjects 

# Terraform variables
Before using this code we need to create terraform.tfvars file which look like terraform-draft.tfvars file in the same location. It is described there what values to provide. We are assigning there values to variables from the variables.tf file located in the same folder. In the variables.tf we can also find descriptions of those variables. We need to assign values only for those variables which doesn't have assigned the default value.
# Terraform configuration
We need to configure properly Terraform on our computer so it can create resources in our Azure subscription, it is described here: [developer.hashicorp.com](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/azure-build).
# Azure subscription
We need to have a subscription on the Azure platform portal.azure.com.