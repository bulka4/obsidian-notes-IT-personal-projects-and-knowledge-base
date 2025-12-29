Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
Modules allow us to reuse code in multiple projects. There are different kinds of modules which differ in from where we are taking a code:
- Local modules
	- Source: A directory on a local filesystem
- Git based modules
	- Source: A git repository
- Terraform registry modules
	- Source: Terraform registry, public or private
- Private registry modules
	- Source: A private Terraform module registry (e.g., inside Terraform Cloud or Terraform Enterprise).

Each module has defined its own variables and outputs.

When creating a module, we need to provide all the necessary variables.

After creating a module, we can access its outputs.

For example, we can have local modules like that:
![[2 - Images/Terraform/Screenshot 1.png]]

Here we have a separate module for creating different Azure resources, linux VM, networks, resource group, storage account and generating SSH keys.

Those modules can be then used in scripts in a repo like this:
![[2 - Images/Terraform/Screenshot 2.png]]
# Modules
- Local modules - [[Terraform - Local modules]]
- Git based modules - [[Terraform - Git based modules]]
- Private registry modules - [[Terraform - Private registry modules]]
## Providers in modules
Sometimes in the module we need to specify providers even though we have those providers defined in the root module.

#Cloud #DevOps #InfrastructureEngineering #Terraform 