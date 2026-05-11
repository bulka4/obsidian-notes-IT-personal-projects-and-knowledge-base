Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
The Terraform module `modules/ssh` can be used to:
- Generate SSH keys pair (as strings)
- Save the private key on our local computer
- Add the public key to the authorized keys on the created VMs

Public and private keys will be used for connecting to the created VMs.
# Where to save the private key
The `ssh_path` Terraform variable specifies where on our local computer the private key will be saved. 

The recommended one for Windows is `C:\Users\username\.ssh\id_rsa` (if we save the private key here then we don't need to provide a path to that key when running the `ssh` command).