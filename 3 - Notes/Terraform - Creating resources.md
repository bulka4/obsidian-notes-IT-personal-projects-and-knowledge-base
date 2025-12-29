Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
We need to prepare a set of .tf files in a repository. In those files we specify what resources we want to create. We can create multiple files creating different resources.

Then we need to create a plan about what resources will be built. For that we need to run:
- terraform plan -out main.tfplan

That will create a plan and save it in the main.tfplan file.

After that we run this command:
- terraform apply

In order to execute the plan and create all the resources specified in all the .tf files in our repository.

#Cloud #DevOps #InfrastructureEngineering #Terraform 