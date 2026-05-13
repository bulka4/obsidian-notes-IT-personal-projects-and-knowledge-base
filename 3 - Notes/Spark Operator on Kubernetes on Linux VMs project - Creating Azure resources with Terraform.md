Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In the `terraform_linux_vm` folder we have terraform code which:
- Creates VMs
- Configures Spark and Kubernetes on them by executing bash scripts
- Creates ACR for storing Docker images
# Terraform file structure
- `main.tf` - The main script creating all the resources
- `terraform_linux_vm > modules` folder - Folder with modules for creating different resources used in the `main.tf`
# Terraform outputs
[[Spark Operator on Kubernetes on Linux VMs project - Terraform outputs]]
# SSH key generation
Terraform generates SSH keys - [[Spark Operator on Kubernetes on Linux VMs project - Generating SSH keys]].
# ACR setup
[[Spark Operator on Kubernetes on Linux VMs project - ACR setup]]
# VMs setup
[[Spark Operator on Kubernetes on Linux VMs project - Terraform - VMs setup]]