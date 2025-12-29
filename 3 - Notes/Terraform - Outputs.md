Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Creating outputs

In terraform we can create outputs. In order to do that we need to write such a command in out .tf file:
```
output "output_name" {
	value = "some_value"
	description = "description"
}
```

Further sections of this document explains how we can use outputs.
# Using outputs in modules

In Terraform I can create modules. Every module is a directory containing multiple .tf files. For example we might have a structure like this:
  
terraform-modules/

├── main.tf                 # Parent module

├── variables.tf

├── outputs.tf

└── modules/

    └── s3_bucket/          # Child module

        ├── main.tf

        ├── variables.tf

        └── outputs.tf

So here we are creating a child module called ‘s3_bucket’.

This module can create output values. They are defined in the modules/s3_bucket/outputs.tf file. This file can look for example like that:

modules/s3_bucket/outputs.tf :
```
output "bucket_arn" {
	value = aws_s3_bucket.this.arn
}
```

In order to access this module’s output in the parent module we need to define that module at first in the main.tf file in the parent module:

Main.tf file:
```
module "my_s3_bucket" {
	source = "./modules/s3_bucket"
	bucket_name = "my-unique-bucket-name-1234"
	environment = "dev"
}
```

So here we are creating a module called ‘my_s3_bucket’.

Now in the parent module we can use output from the child module by using command:
- module.my_s3_bucket.bucket_arn.

We can use that output from the child module for example in output of the parent module. In that case we can create the output of the parent module in the file called output.tf:

Output.tf file:
```
output "s3_bucket_arn" {
	value = module.my_s3_bucket.bucket_arn
}
```

#Cloud #DevOps #InfrastructureEngineering #Terraform 