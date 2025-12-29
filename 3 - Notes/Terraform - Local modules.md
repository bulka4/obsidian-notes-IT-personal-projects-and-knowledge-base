Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
Local modules are saved in a directories on our local filesystem.

When creating a local module, as a source argument we are providing a path to a local directory containing this module.

For example if we have a repo like this:
```
|- terraform_repo
	|- modules
		|- networks
		|- resource_group
	|- main.tf
```

Then we specify a source for a module in the main.tf file like this:
```
module "network" {
	source = "./modules/network"
}
```

#Cloud #DevOps #InfrastructureEngineering #Terraform 