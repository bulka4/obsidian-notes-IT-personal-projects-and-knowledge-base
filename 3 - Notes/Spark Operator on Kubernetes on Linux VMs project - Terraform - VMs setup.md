Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
The `terraform_linux_vm > modules > linux_vm > main.tf` script contains code creating VMs.

We are creating VMs of specified size (Standard_B2ms by default) and we create on them a new user specified by the `vm_username` variable.
# VMs network setup
Terraform creates networks (Vnets) for our VMs. They will get assigned public IP addresses and we can define for them security rules.

In the `terraform_linux_vm > modules > networks > main.tf` we are defining security rules for our VMs network. We open there specific ports required to run Kubernetes, to be able to connect through SSH and to access a Jupyter Notebook from a browser on our local computer.

This networking setup is crucial to make sure that Kubernetes cluster works properly. When creating those networking rules, we need to take into account among the others what CNI we are using in our Kubernetes cluster (Calico in this case).
# VMs configuration using bash scripts
Terraform runs bash scripts (saved in `terraform_linux_vm > bash_scripts`) on VMs which sets up Jupyter Notebook and Kubernetes on them.

More info is here - [[Spark Operator on Kubernetes on Linux VMs project - VMs configuration]].