Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes Terraform code from this RAG app project - [[RAG app project|link]].

Terraform code creates the following resources in Azure:
- AKS
- ACR – For storing images we will be deploying on AKS
- Service Principal – Used for authentication when:
    - Pulling and pushing images to ACR
    - Interacting with AKS using kubectl (creating the kubeconfig file)
- File share – Which will be mounted to AKS pods and contain application files

And saves on the local computer the following files (terraform inserts into them proper value about created resources in Azure):
- interacting.aks.Dockerfile – Used for building a Docker image for interacting with AKS
- Dockerfiles:
    - For MCP Server (apps/mcp_server/Dockerfile)
    - For preparing Milvus db (apps/prepare_milvus_db/Dockerfile)
- Values.yaml – Files used in all the Helm charts: Common, MCP Server, Prepare Milvus db and Ray Service. Terraform inserts into those files values for:
    - ACR URL
    - Service Principal client name and password