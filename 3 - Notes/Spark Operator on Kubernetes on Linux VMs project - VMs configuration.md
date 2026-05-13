Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Terraform runs bash scripts (saved in `terraform_linux_vm > bash_scripts`) on VMs which:
- Prepares a Docker image ([[Spark Operator on Kubernetes on Linux VMs project - Docker image for Spark and Jupyter Notebook|link]]) for:
	- Running Jupyter Notebook ([[Spark Operator on Kubernetes on Linux VMs project - Jupyter Notebook setup|link]])
	- Running Spark in both local and cluster mode
- Runs Jupyter Notebook in a container using prepared image
- Configures Kubernetes ([[Spark Operator on Kubernetes on Linux VMs project - Kubernetes cluster setup|link]])
- Prepares Kubernetes resources needed to run Spark scripts using Spark Operator ([[Spark Operator on Kubernetes on Linux VMs project - Preparing Spark Operator and `SparkApplication` CRD|link]])
# Azure VM Extension
To execute bash scripts on VMs, we use the `azurerm_virtual_machine_extension` Terraform resource which uses Azure VM Extension.
# Bash scripts - actions performed - details
We have two scripts:
## vm1_configure.tftpl
Script executed on the VM1. It performs the following actions:
- Installs Docker
- Creates a Dockerfile and the `entrypoint.sh` script used in this Dockerfile
- Builds an image from it and pushes it to ACR
- Runs a container which:
	- Contains Spark setup to run in a local mode
	- Runs Jupyter Notebook
- Prepares a sample Spark script to test if it works
- Configures Kubernetes (that VM acts as a Master node)
	- Prepares the `/home/azureadmin/k8s_join_workers.txt` script with a join command for adding the other VM to the Kubernetes cluster
- Installs Spark Operator using Helm
- Patches Spark Operator deployments to add necessary tolerations (more details in code comments)
- Creates a Service Account used by Spark Driver Pod
- Creates a Secret used for authentication to ACR for pulling Docker image
- Prepares SparkApplication manifest (which will be used for submitting Spark jobs)
## vm2_configure.tftpl
Script executed on the VM2. It performs the following actions:
- Configures Kubernetes (that VM acts as a Worker node)
- Prepares a sample Spark script to test if it works
# Rendering bash scripts by Terraform
Those bash scripts can't be used on their own on a Linux machine since they are rendered using the Terraform templatefile function first before execution. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/functions/templatefile).

We are inserting into those scripts variables specified in the templatefile function (what can be found in the terraform_linux_vm > main.tf script) and also we are using there escape sequences. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/expressions/strings).

Logs from executing a bash script on VM can be found on that VM in the /var/lib/waagent/custom-script/download/0/ folder. There are the 'stdout' and 'stderr' files with logs. More info about that here: [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/troubleshoot).