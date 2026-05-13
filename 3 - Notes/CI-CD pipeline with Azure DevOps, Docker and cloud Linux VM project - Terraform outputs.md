Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
Terraform code creates a few outputs which we are gonna need:
- `public_ip_address` - Public IP address of the created VM
- `sp_id` - app / client ID of the created Service Principal
- `sp_password` - password of the created Service Principal
- `tenant_id` - ID of the Tenant of the created Service Principal

Those outputs will be printed in a console once the 'terraform apply' command is finished. We can also access those values using one of those commands:
```
terraform output # print all the outputs
terraform output -raw <output-name> # print a specific output
```

The `sp_password` output is sensitive so it won't be printed in a console. In order to get its value we need to use the `terraform output -raw <name>` command for getting a specific output.
# Preparing `.env` files
Terraform outputs will be needed to prepare `.env` files as described here - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Prerequisites|link]].