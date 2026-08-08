Tags: [[__My_projects]]
#MyProjects 

# Introduction
We use kind (local Kubernetes cluster running in Docker containers) to run this system. There is also a Docker image for interacting with it ([[Data governance app with a RAG system - Docker image for interacting with kind|link]]) (which allows to use `kubectl` and `helm` commands among others).
# Starting the cluster
We start the cluster using this command:
```bash
# Run this from the repo root folder
kind create cluster --name data-gov --config kind-config.yaml
```
# Kubeconfig file
A kubeconfig file, needed to interact with the cluster, is saved in the `%USERPROFILE%\.kube\config` file (`%USERPROFILE%` is user's folder, for example `C:\Users\<user-name>`) automatically by kind when we create a cluster.
# Docker image for interacting with kind
We can use a Docker image to interact with the kind cluster (it contains set up `kubectl` and `helm` among others). More info about it is here - [[Data governance app with a RAG system - Docker image for interacting with kind|link]].
# Docker images to be used for deploying pods
In the image for interacting with kind ([[Data governance app with a RAG system - Docker image for interacting with kind|link]]) we create a script `/root/dockerfiles/build_and_load.sh` for building Docker images and loading them to kind, so they can be used for deploying pods.

We need to run commands from this script on the host, outside of the image for interacting with Kubernetes (because it requires Docker).

We need to use `image_pull_policy="IfNotPresent"` option when creating a pod to use a local image instead of pulling one from a remote registry.