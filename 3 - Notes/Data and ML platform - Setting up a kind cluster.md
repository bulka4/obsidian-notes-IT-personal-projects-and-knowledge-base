Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
This document describes how setting up a kind cluster works in this repo - [link](https://github.com/bulka4/data_and_ml_platform_kind).
# Kubeconfig file
A kubeconfig file, needed to interact with the cluster, is saved in the `%USERPROFILE%\.kube\config` file (`%USERPROFILE%` is user's folder, for example `C:\Users\<user-name>`) automatically by kind when we create a cluster.
# Docker image for interacting with the kind cluster
We create a Docker image with prepared tools for interacting with the kind cluster. We use for that the `interacting.kind.Dockerfile` Dockerfile.

The image will include:
- `kubectl`
- `helm`
- Scripts for:
	- Building Docker images and loading them to kind (more info in the next section 'Docker images to be used for deploying pods')
	- Creating Kubernetes namespaces and secrets

We mount into that image the kubeconfig file for our kind cluster in the `/root/.kube` folder so we can use `kubectl` for interacting with the kind cluster.
# Docker images to be used for deploying pods
In the image for interacting with kind we create a script for building Docker images and loading them to kind.

We build Docker images locally and load them to kind so they can be used for deploying pods in kind.

We might need to use `image_pull_policy="IfNotPresent"` option to use a local image instead of pulling one from a remote registry.