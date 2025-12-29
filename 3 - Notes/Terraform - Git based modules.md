Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
We can have a Terraform module saved in a Git repository and access it directly in another repository:
```
module "aks" {
	source = "git::https://github.com/..."
}
```
## Terraform registry modules
There are available modules on the Terraform Registry website [registry.terraform.io](https://registry.terraform.io/).

We create a module from a Terraform Registry like this:
```
module "vpc" {
	source = "terraform-aws-modules/vpc/aws"
	version = "5.0.0"
}
```

#Cloud #DevOps #InfrastructureEngineering #Terraform 