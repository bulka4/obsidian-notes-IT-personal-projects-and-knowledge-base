Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

## Confidential variables
Instead of storing confidential variables in the .env file in the dags/project_1 folder it would be better to store them somewhere where they can be accessed remotely, for example in Azure Key Vault and access them using Azure Rest API or Azure SDK.

Using .env file will not be practical when we want to deploy our app. We can't place that file in the repository from which code will be deployed using a CI/CD pipeline.