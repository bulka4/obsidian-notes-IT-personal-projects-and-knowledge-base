Tags: [[__My_projects]]
#MyProjects 

# Introduction
We can create a Docker image with prepared tools for interacting with the kind cluster ([[Data governance app with a RAG system - Kind (kubernetes cluster in Docker)|link]]). 

This image includes:
- `kubectl`
- `helm`
- Scripts for:
	- Building Docker images and loading them to kind (more info in the next section 'Docker images to be used for deploying pods')
	- Creating Kubernetes namespaces and secrets

From inside of that image we perform operations like:
- Deploying Helm charts
- Interacting with Kubernetes pods (checking statuses, logs, connecting to them and executing CLI commands)
# Usage
In order to use it:
- Copy the `.kube` folder (usually located at `C:\Users\username`) into the repo root folder (so it can be copied into the image we build in the next step)
- Build and run the image for interacting with kind ([[Data and ML platform project - Docker image for interacting with AKS|link]]):
```bash
# Run this from the repo root folder
docker build -t interacting-kind -f interacting.kind.Dockerfile .
docker run -it --rm interacting-kind bash
```
# Loading Docker images to kind
We can use the `/root/apps/build_and_push.sh` script from the image to build images and load them to kind which are needed to create pods.

We need to run commands from this script on the host as they requires Docker.
# Creating Kubernetes namespaces and secrets
The `/root/create_k8s_secrets.sh` script can be used to create Kubernetes namespaces and secrets we will be using later to run applications.
# Helm charts
In the `/root/helm_charts` folder we have Helm charts copied from the host which we can run on kind.