Tags: [[__My_projects]]
#MyProjects 

# Introduction
This is a guide for how to set up all the infrastructure needed to run the code from this repo - (link) on a kind cluster for development.

We assume here that we already have:
- Azure account
- Terraform, Docker and kind installed
# Kind cluster setup
Set up a kind cluster and Docker image for interacting with it ([[Data governance app with a RAG system - Kind (kubernetes cluster in Docker)|link]], [[Data governance app with a RAG system - Docker image for interacting with kind|link]]):
- Start Docker engine
- Run this command:
```bash
# Run this from the repo root folder
kind create cluster --name data-gov --config kind-config.yaml
```
- Copy the `.kube` folder (usually located at `C:\Users\username`) into the repo root folder (so it can be copied into the image we build in the next step)
- Build and run the image for interacting with kind:
```bash
# Run this from the repo root folder
docker build -t interacting-kind -f interacting.kind.Dockerfile .
docker run -it --rm interacting-kind bash
```
# (Optional) VS Code for code development on Kubernetes
If we want to use VS Code to connect to Kubernetes pods and be able to modify files there and run commands in a terminal, we need to additionally modify the kubeconfig file to allow VS Code to connect to the Kubernetes cluster:
- Kubeconfig file is usually located at `C:\Users\username\.kube\config`)
- We need to modify it and change the IP address from `0.0.0.0` to `127.0.0.1` in the `clusters.cluster_name.server` field, for the kind cluster.
# Cleanup
How to clean up resources when we are done.

Cleanup of Docker images:
```bash
# remove all containers
docker rm $(docker ps -aq)

# remove all images
docker rmi $(docker image ls -aq)

# remove build cache
docker image prune -a
docker builder prune -a

# remove everything (images, containers, cache, volumes)
docker system prune --all --volumes
```

Delete the kind cluster:
```bash
kind delete cluster --name data-platform
```
# Prepare images and Kubernetes secrets
From inside of the image for interacting with Kubernetes:
- Run the `/bin/sh /root/create_k8s_secrets.sh` command
	- To create Kubernetes namespaces and secrets we will be using
- Run commands from the `/root/dockerfiles/build_and_load.sh` script on the host (run them outside of the image for interacting with kind. They require to use Docker)
	- It builds Docker images and loads them to kind, so they can be used to run pods
# Installing Helm charts
