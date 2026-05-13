Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
After creating VMs using Terraform we are executing on them bash scripts using the azurerm_virtual_machine_extension Terraform resource which uses Azure VM Extension.

Those bash scripts are used to configure both VMs for running Hadoop. They can't be used on their own on a Linux machine since they are rendered using the Terraform templatefile function first before execution. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/functions/templatefile).

We are inserting into those scripts variables specified in the templatefile function (what can be found in the `terraform_linux_vm > main.tf` script) and also we are using there escape sequences. More information about that here [developer.hashicorp.com](https://developer.hashicorp.com/terraform/language/expressions/strings).

Logs from executing a bash script on VM can be found on that VM in the `/var/lib/waagent/custom-script/download/0/` folder. There are the 'stdout' and 'stderr' files with logs. More info about that here: [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/troubleshoot).