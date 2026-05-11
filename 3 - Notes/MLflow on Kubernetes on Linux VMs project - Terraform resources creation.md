Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We use Terraform to prepare infrastructure in Azure. The entire code for that is in the `terraform_linux_vm` folder. It performs the following actions:
- Creating a Resource Group
- Creating ACR - For storing Docker Images used in Kubernetes
- Creating Service Principal - used for authentication when pulling/pushing Images to ACR
- Generating SSH keys pair - It will be used for connecting to created VMs from our local computer
- Creating a Storage Account - It will be used as an artifact store for MLflow Tracking Server
- Creating two Linux VMs - Called VM1 and VM2 on which we will run Kubernetes cluster and MLflow
- Configuring both VMs - by executing on them bash scripts `vm1_configure.tftpl` and `vm2_configure.tftpl` from the `terraform_linux_vm > bash_scripts` folder.
# Terraform outputs
Terraform creates the following outputs: 
- `public_ip_address_vm_1` and `public_ip_address_vm_2` - Public IP addresses of both VMs
- `acr_sp_id` and `acr_sp_password` - Credentials used for authentication to ACR.

They are printed at the end of executing 'terraform apply' and they can be accessed by running the command:
>terraform output
# SSH key generation
Terraform is used to generate SSH keys to connect to created VMs as described here - [[MLflow on Kubernetes on Linux VMs project - Generating SSH keys|link]].
# ACR setup
ACR is created using the `terraform_linux_vm > modules > acr` module. We are also creating a Service Principal which will be used for authentication to it using the `service_principal` module.
# VMs setup
Terraform creates and configures VMs like described here - [[MLflow on Kubernetes on Linux VMs project - Terraform VMs setup]]
