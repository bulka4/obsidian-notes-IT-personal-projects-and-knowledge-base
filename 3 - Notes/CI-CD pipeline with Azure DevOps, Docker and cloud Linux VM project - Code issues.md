Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Pushing code to ACR in CI/CD pipeline doesn't work
When we run a CI/CD pipeline using resources prepared by this code, we get an error that we are not authorized to push a Docker image to ACR.

This will be related to the Service Connection which we create in DevOps and Service Principal which is used to create that Service Connection. That Service Connection is used for authentication when pushing imaged to ACR.

That code was working before. I am not sure what might be wrong. It might be worth to create a Service Connection manually using our Service Principal. If that works, then that means that the Rest API call which we make to create that Service Connection automatically doesn't work.