Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Terraform creates the following outputs:
- public_ip_address_vm_1 and public_ip_address_vm_2 - Public IP addresses of both VMs
- acr_sp_id and acr_sp_password - Credentials used for authentication to ACR.

They are printed at the end of executing 'terraform apply' and they can be accessed by running the command:
```
terraform output
```