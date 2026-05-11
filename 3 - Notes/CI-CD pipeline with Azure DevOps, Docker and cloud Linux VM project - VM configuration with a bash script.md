Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
The `terraform > install_tools.sh.tftpl` file is a bash script template which will be executed on the created VM and will install on it:
- Docker - Which will be used to run an app in a container
- Self Hosted Agent - Needed to perform actions from a CI/CD pipeline ([[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Pipeline design|link]])
## Azure VM Extension
It is executed using the `azurerm_virtual_machine_extension` Terraform resource which uses Azure VM Extension.
## Rendering
That bash script can't be used on its own on a Linux machine since it is rendered using the Terraform templatefile function first before execution. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/functions/templatefile).

We are inserting into that script variables specified in the templatefile function (what can be found in the terraform > main.tf script) and also we are using there escape sequences. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/expressions/strings).

Logs from executing a bash script on VM can be found on that VM in the /var/lib/waagent/custom-script/download/0/ folder. There are the 'stdout' and 'stderr' files with logs. More info about that here: [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/troubleshoot).