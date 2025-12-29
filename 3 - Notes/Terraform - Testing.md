Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]], [[_Terraform]]

# Introduction
There are tools helping with testing if our code is correct. Not only if that code will work without errors but if it is gonna work as excpected and we are not violating any common rules.

# Third-party testing tools
- TFLint - [[Terraform - Testing with TFLint]]
- Checkov - [[Terraform - Testing with Checkov]]
# Terraform native testing tools
### Check block
Check blocks are used to check if resources have been created correctly. They use the data block to get information about the created resources.
### Lifecycle block
Lifecycle blocks can be used to check if all requirements are met before creating resources, and like check blocks they can check if resources have been created properly.
### Assert block
Assert block can be used for testing our code.
### Mocking
There is the mocking option in Terraform for testing our code.
### Variables validation
We can use the validation argument in a variable in order to validate if the entered values for that variable is correct.
### Terraform test cli
There is the Terraform test cli tool which can be used for testing as well.

#Cloud #DevOps #InfrastructureEngineering #Terraform 