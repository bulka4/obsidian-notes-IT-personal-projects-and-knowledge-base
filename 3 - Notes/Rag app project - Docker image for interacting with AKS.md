Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes the Docker image for interacting with AKS used in this project - [[RAG app project|link]]. 

The /interacting.aks.Dockerfile is used for creating an image used for interacting with AKS and it will be prepared by Terraform code.

This Dockerfile is created by Terraform by interpolating a template of this Dockerfile, saved in the terraform > template_files > docker > template.interacting.aks.Dockerfile. Created Dockerfile will be saved in the repository root folder.

This image can be used in order to:
- Build and push to ACR images we will be deploying on AKS
    - Image will contain Dockerfiles and script for building and pushing images to ACR (this script will be ran when container starts)
- Interacting with AKS using kubectl. In the image we will have:
    - Kubectl configured
    - Helm installed
    - Helm charts from the repo for deploying MCP server, preparing Milvus db and Ray Serve app serving LangGraph graph (agent)