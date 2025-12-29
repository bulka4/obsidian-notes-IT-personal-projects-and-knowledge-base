Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
- Init Terraform in a folder (we need to do this before we run a Terraform file located in that folder):
	- cd directory_name
	- terraform init
- Create and destroy resources defined in the Terraform file:
	-  terraform apply # create or modify resources
	- terraform destroy # destroy resources
- Create and destroy resources defined in the Terraform file with execution plan:
	- terraform plan -out main.tfplan # create execution plan
	- terraform apply # create or modify resources
	- terraform plan -destroy -out main.destroy.tfplan # create execution plan
	- terraform apply main.destroy.tfplan
- Get output value:
	- Terraform output -raw output_name
	- Terraform output
	- Terraform output -json

#Cloud #DevOps #InfrastructureEngineering #Terraform 