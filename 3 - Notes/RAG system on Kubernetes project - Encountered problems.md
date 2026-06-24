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
# Encountered problems
## Learning new concepts
I needed to learn a lot of new things:
- Indexes in a vector database (Milvus)
- Ray Serve (the most difficult one)
- Asynchronous functions in Python
## Making the `answer_agent` function asynchronous
I made the `answer_agent` function asynchronous, so it can run in parallel with other asynchronous functions.

I made it asynchronous by using commands:
```python
loop = asyncio.get_event_loop()
answer = await loop.run_in_executor(...)
```
## Ray Serve app
### Initiating RAG workflow
I needed to make sure that we load LLM only once, when we start the HTTP server, not every time when someone makes a request.
### Kubernetes deployment
I needed to configure the `RayService` CRD to define how to run Ray Service on Kubernetes. I needed to convert my RAG app into a `.zip` file in order to run it.
## Architecture design
I needed to decide where to convert question into an embedding - on the MCP server or in the app with the `LangGraph` workflow.

I have chosen the MCP server to create a clear separation of responsibilities:
- MCP server does all the heavy computations
- Other applications that uses this MCP server do only light computations. They mainly deal with request handling.