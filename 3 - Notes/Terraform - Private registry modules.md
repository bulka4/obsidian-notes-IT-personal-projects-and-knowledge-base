Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
We can create a private Terraform module registry for example inside Terraform Cloud or Terraform Enterprise.

We create a module from a private registry like this:
```
module "vpc" {
	source = "app.terraform.io/my-org/network/azure"
	version = "5.0.0"
}
```

#Cloud #DevOps #InfrastructureEngineering #Terraform 