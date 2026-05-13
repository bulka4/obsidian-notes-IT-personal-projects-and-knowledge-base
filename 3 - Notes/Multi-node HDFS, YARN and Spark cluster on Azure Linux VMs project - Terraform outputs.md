Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Terraform creates two outputs: `public_ip_address_vm_1` and `public_ip_address_vm_2` which we will need to connect to created VMs using SSH.

They are printed at the end of executing `terraform apply` and they can be accessed by running the command:
```
terraform output
```