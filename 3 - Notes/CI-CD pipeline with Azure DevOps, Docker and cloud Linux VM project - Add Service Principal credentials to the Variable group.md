Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
The `acr_push_and_pull > setup.py` script creates a variable group with a specified name and create there variables:
- `SP_ID` - Equals to a Service Principal application ID
- `SP_PASSWORD` - Equals to a Service Principal password 

Those variables are used in the YAML file defining a CI/CD pipeline in order to authenticate when pulling a Docker image from ACR. 

We are including this variable group name this way:
```yaml
variables:
	- group: ACR-SP-credentials
```

This will allow to access variables `SP_ID` and `SP_PASSWORD` which are used in the bash script which is pulling Docker image onto the VM:
```yaml
- stage: Deploy
  jobs:
	  - job: PullImage
	    steps:
		    - script: |
		      image_name=dataEngineeringApps.azurecr.io/airflow:$(Build.BuildId)
		      
		      # Set the Azure Pipeline variables as environment variables. They
		      # will be used later on
		      export CONTAINER_REGISTRY=dataEngineeringApps.azurecr.io
		      export IMAGE_REPOSITORY=airflow
		      export IMAGE_TAG=$(Build.BuildId)
		      
		      echo "Login to Docker using Service Principal credentials"
		      docker login dataEngineeringApps.azurecr.io \
		      -u $(SP_ID) -p $(SP_PASSWORD)
```