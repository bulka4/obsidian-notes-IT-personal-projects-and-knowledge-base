Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
After creating VMs using Terraform we are executing on them bash scripts from the `terraform_linux_vm > bash_scripts` folder 
# Azure VM extension
Bash scripts are being executed on VMs by Terraform using the `azurerm_virtual_machine_extension` Terraform resource which uses Azure VM Extension.
# Actions performed by bash scripts
Those bash scripts performs the following actions:
- Configuring the Kubernetes cluster
- Installing Docker
- Prepare YAML manifests and scripts for deploying Kubernetes resources
	- MLFlow Tracking Server
	- Example Python script to test connectivity to the Tracking Server
- Create the `/home/azureadmin/k8s/mlflow_deploy.sh` script which contains code for deploying all the Kubernetes resources:
	- Namespace
	- Volume for MySQL
	- MySQL
	- Secrets
	- MLflow Tracking Server Pod with a Service
- Create a Docker image for MLflow Tracking Server and push it to ACR

Those bash scripts can't be used on their own on a Linux machine since they are rendered using the Terraform templatefile function first before execution. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/functions/templatefile).

We are inserting into those scripts variables specified in the templatefile function (what can be found in the terraform_linux_vm > main.tf script) and also we are using there escape sequences. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/expressions/strings).

Logs from executing a bash script on VM can be found on that VM in the /var/lib/waagent/custom-script/download/0/ folder. There are the 'stdout' and 'stderr' files with logs. More info about that here: [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/troubleshoot).