Tags: [[_My_projects]]
#MyProjects 

# Introduction
Terraform creates a Dockerfile which can be used to build an image from which we can interact with AKS and ACR through CLI using:
- Helm
- kubectl
- Azure CLI

From inside of that image we perform operations like:
- Building Docker images and pushing them to ACR
- Deploying Helm charts
- Interacting with Kubernetes pods (checking statuses, logs, connecting to them and executing CLI commands)
# Pushing Docker images to ACR
We can use the `/root/apps/build_and_push.sh` script from the image to build images needed for the platform and push them to ACR.
# Helm charts
In the `/root/helm_charts` folder we have all the Helm charts copied from the repository.
