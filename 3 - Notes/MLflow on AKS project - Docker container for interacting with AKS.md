Tags: [[_My_projects]]
#MyProjects 

# Introduction
Terraform code will generate a Dockerfile and save it in the docker folder in this repository. Docker image created by this Dockerfile is used to:
- Build and push to ACR Docker images
    - It is done when starting a container
    - Those images will be used for deploying the MLflow Tracking Server and running the project
- Install Helm charts:
    - For deploying Tracking Server
    - For running MLflow project
- Interact with AKS using kubectl

In this image we are going to have:
- Installed Azure CLI - Which will be used to:
    - Get credentials to AKS (create the .kube/config file) what will enable using kubectl
    - Push images to ACR
- Installed and configured kubectl:
    - We will have prepared the .kube/config file used for authentication to AKS which enables us using kubectl.
- Installed Helm
## Build and push to ACR Docker images
When starting a container for interacting with AKS, the build_and_push.sh bash script will be executed which will build and push to ACR Docker images.

This script is using files from the docker > mlflow_docker folder (which is copied from the repo into the image). In this folder we have Dockerfiles for building images and other files used by those Dockerfiles.

We build two images:
- **Image for running MLflow project**
    - It contains Python installed and all the libraries used in the project
    - For building it we use the mlproject.Dockerfile and mlproject_requirementx.txt files
    - The mlproject_requirementx.txt contains Python libraries needed to run the project
- **Image for deploying MLflow Tracking Server**
    - For that we use the tracking-server.Dockerfile file
    - It has installed packages needed to run the Tracking Server which uses Azure Storage Account as an artifact store and MySQL as a backend store.
## Service Principal for permissions
When building this Docker image we will run the following Azure CLI commands:
- `az aks get-credentials` - To create the kubeconfig file (.kube/config). That will allow us to use kubectl to interact with our AKS cluster.
- `az acr build` - To build and push to ACR Docker images.

Running those commands requires proper permissions. That's why, when building this image, we need to login to Azure using `az login` using a Service Principal with proper roles and scopes:
- Role 'Contributor' with scope for ACR - Enable pushing images to ACR using the `az acr build` command
- Role 'Azure Kubernetes Service Cluster User Role' with scope for AKS - Enable getting credentials to AKS (creating .kube/config file) using the `az aks get-credentials` command