Tags: [[_My_projects]]
#MyProjects 

# Introduction
**GitHub link**: [link](https://github.com/bulka4/rag_ai_agent)
**Key technologies**: LangGraph, MCP, vector database (Milvus), FastAPI, Ray, Terraform, Kubernetes, Helm, Docker, Azure Container Registry

In this project I have created a RAG (Retrieval-Augmented Generation) application that answers users' questions based on the available documentation. It works in the following way:
- User submits a question
- Documents relevant to this question are retrieved using semantic search
- Response is generated using retrieved documents

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
- Build a Docker image for interacting with Azure resources (e.g. pushing images to ACR, creating Kubernetes resources using kubectl)
- Upload application files to Azure File share and mount them to Kubernetes pods, allowing for changing code without rebuilding images

**Outcome**
After deployment, application is running on a Kubernetes cluster in Azure and it can handle requests from other servers providing answers to questions.
# Additional information
To learn more about this project, refer to the documents with link listed below:
- [[Rag app project - Architecture]]
- [[Rag app project - Deployment guide]]
- [[Rag app project - Docker image for interacting with AKS]]
- [[Rag app project - Apps]]
- [[Rag app project - Dockerfiles]]
- [[Rag app project - Testing app deployment using Docker compose]]
- [[Rag app project - Helm charts]]
- [[Rag app project - Terraform]]
# Next steps plan
More information about the Next steps plan regarding this project - [[RAG app project - Next steps plan]].