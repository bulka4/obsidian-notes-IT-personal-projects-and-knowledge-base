Tags: [[__My_projects]]
#MyProjects 

# Introduction
**Key technologies**: LangGraph, MCP, vector database (Milvus), FastAPI, Ray Serve, Terraform, Kubernetes, Helm, Docker, Azure Container Registry

**Goal**
In this project I have created a RAG (Retrieval-Augmented Generation) application that answers users' questions based on the available documentation. It works in the following way:
- One LLM converts user’s question into a vector embedding
- Documents relevant to this question are retrieved from a vector database (semantic search)
- Another LLM generates a response using retrieved documents
 
**Architecture overview**
Here are the most important components of this RAG system:
- Multi-agent workflow created using LangGraph
- MCP server providing a tool for semantic search
- Vector database used for storing document embeddings
- FastAPI + Ray Serve to serve it as Rest API

**Deployment overview**
This project includes files enabling automatic deployment of the application on AKS (Azure Kubernetes Service):
- Terraform - Creates Azure resources (AKS and more)
- Helm charts - Create resources on AKS

**Code development**
To simplify code development, this project gives a possibility to:
- Build a Docker image for interacting with Azure resources (e.g. pushing images to ACR, creating Kubernetes resources using `kubectl`)
- Upload application files to Azure File share and mount them to Kubernetes pods, allowing for changing code without rebuilding images

**Outcome**
After deployment, application is running on a Kubernetes cluster in Azure and it can handle requests from other servers providing answers to questions.
# Code repository
Repository with project's code - [github.com](https://github.com/bulka4/rag_system_kubernetes).
# Infrastructure
Additional information about preparing infrastructure:
- [[RAG system on Kubernetes project - Docker image for interacting with AKS]]
- [[RAG system on Kubernetes project - Terraform]]
- [[RAG system on Kubernetes project - Helm charts]]

App deployment guide:
- [[RAG system on Kubernetes project - Deployment guide]]
- [[RAG system on Kubernetes project - Testing app deployment using Docker compose]]
# Application architecture and code
Additional information about application architecture and code:
- [[RAG system on Kubernetes project - Architecture]]
- [[RAG system on Kubernetes project - Apps]]
- [[RAG system on Kubernetes project - Dockerfiles]]
# Next steps plan
More information about the Next steps plan regarding this project - [[RAG system on Kubernetes project - Next steps plan]].