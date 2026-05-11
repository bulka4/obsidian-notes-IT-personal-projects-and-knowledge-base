Tags: [[_My_projects]] [[__Machine_Learning]]
#MyProjects #MachineLearning 

# Introduction
The CI/CD pipeline which we can build using infrastructure prepared using code from this repository performs the following actions:
- Wait until we push code to the repo
- Once the code is pushed, build a Docker image using a Dockerfile included in the repo
- Push this Docker image to ACR (Azure Container Registry)
- Pull the Docker image from ACR onto Azure Linux VM
- Run a container using the pulled Docker image and docker-compose.yaml file from the repo on this VM
# Self Hosted Agent
All the actions performed by this pipeline are done by a Self Hosted Agent from Azure Pipelines which is installed on this VM by a bash script executed by Terraform ([[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - VM configuration with a bash script|link]]).
# How Docker image and docker-compose are used
For example, we can have a `docker-compose` file like that:
```yaml
services:
	service_1:
		image: ${CONTAINER_REGISTRY}/${IMAGE_REPOSITORY}:${IMAGE_TAG}
		environment:
			...
		volumes:
			...
		command:
			...
			
	service_2:
		image: ${CONTAINER_REGISTRY}/${IMAGE_REPOSITORY}:${IMAGE_TAG}
		environment:
			...
		volumes:
			...
		command:
			...
```

In that case, we are running two containers (services) which uses the Docker image pulled from the ACR and we execute a specified command to start an app in those containers.

We are using the same Docker image for every container in this example, but this could be extended to multiple, different images.

More details are here - [[CI-CD pipeline with Azure DevOps, Docker and cloud Linux VM project - Dockerfile and docker-compose preparation|link]].