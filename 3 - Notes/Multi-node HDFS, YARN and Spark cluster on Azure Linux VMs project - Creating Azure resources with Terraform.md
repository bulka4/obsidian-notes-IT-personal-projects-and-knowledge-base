Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In the terraform_linux_vm folder we have terraform code which creates our VMs and configures on them Spark and Kubernetes by executing bash scripts on them. 

We have there the `main.tf` file which creates all the resources. That file uses modules defined in the `terraform_linux_vm > modules` folder. Each module is dedicated to creating one type of resource in Azure.