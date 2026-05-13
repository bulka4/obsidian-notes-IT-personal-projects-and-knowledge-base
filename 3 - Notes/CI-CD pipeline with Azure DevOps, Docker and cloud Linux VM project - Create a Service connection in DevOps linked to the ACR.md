Tags: [[__My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
We create a Service Connection in DevOps linked to the ACR which we prepared.

It uses the same Service Principal for authentication which credentials we added to the Variable Group in DevOps Library.

It will be used in the YAML file for authentication when pushing images from the ACR.

Once we create this connection we are adding its ID to the generated YAML file as the `containerRegistry` argument:

YAML file:
```yaml
- stage: Build
  displayName: Build na push stage
  jobs:
	  - job: PullImage
	    displayName: Build and push an image to container registry
	    steps:
		    - task: Docker@2
		      displayName: Build and push an image to container registry
		      inputs:
			      command: buildAndPush
			      repository: airflow
			      dockerfile: $(Build.SourceDirectory)/airflow_app/Dockerfile
			      containerRegistry: a0459bd32-e495-4ccd9-bd94-bf09fd78hf
			      tags: $(Build.BuildId)
```

Note: Every time we create a Service Connection in DevOps, it automatically creates a new Service Principal in Azure with a name of the format `<organization>-<project>-xxx`, where organization and project can be taken from DevOps URL: `dev.azure.com/<organization>/<project>`