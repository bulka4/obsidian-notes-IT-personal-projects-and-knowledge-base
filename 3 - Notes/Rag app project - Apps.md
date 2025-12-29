Tags: [[_My_projects]]
#MyProjects 

# Introduction
In this RAG app project - [[RAG app project|link]], we have the following apps:
- Script preparing vector db - Script for preparing sample data (documents with their embeddings) in a vector db
- MCP server - Providing a tool for semantic search
- Ray Serve app – Providing Rest API serving multi-agent RAG workflow built with LangGraph
## Script preparing Milvus db
The prepare_milvus_db > prepare_milvus_db.py script creates a collection in the Milvus db and saves in it sample data (documents with their vector embeddings) which will be used by the MCP tool for semantic search.

We need to run it before we use RAG workflow.
### Environment variables used:
- MILVUS_HOST – DNS name or IP address of the Milvus db where we store documents used for semantic search.
- MILVUS_COLLECTION_NAME – Name of the Collection in the Milvus db with documents used for semantic search.
- EMBEDDING_FIELD_NAME - Name of the field in the Collection which holds vector embeddings.
- TEXT_FIELD_NAME – Name of the field in the Collection which holds document text.
### Embeddings
We are creating there a few documents with their vector embeddings. The entire documents are converted into a single embedding.
### Index
We are creating the IVF index on the field with vector embeddings. That means that the entire collection will be grouped into a specific number of clusters.

Each time we want to find in this collection vectors similar to the given vector, we will search through not all the clusters but part of it.

We will select a specific number of clusters which centroids (average vectors) are the most similar to the given vector and search through only those clusters.

When creating an index we also specifying what metric will be used for finding similar vectors, which is a cosine similarity in this case.
## MCP server
In the mcp_server > mcp_server.py we create the MCP Server with the tool for semantic search. It will use the Milvus db as a vector db where we will store vector embeddings of documents.

This server is created using FastMCP framework and it is using a HTTP Transport. It allows MCP clients to connect from other servers and without starting the server (server is started separately).

MCP Server and clients using its tools are maintained separately.
### Environment variables used:
- MILVUS_HOST – DNS name or IP address of the Milvus db where we store documents used for semantic search.
- MILVUS_COLLECTION_NAME – Name of the Collection in the Milvus db with documents used for semantic search.
- EMBEDDING_FIELD_NAME - Name of the field in the Collection which holds vector embeddings.
- TEXT_FIELD_NAME – Name of the field in the Collection which holds document text.
## Ray Serve app
In the ray_serve_app folder we have files for the Ray Serve app:
- Rag_workflow.py
- Ray_serve_app.py

Both are described in more detail below.
### Rag_workflow.py
Script where we define the RAGWorkflow class. This class is used for running the multi-agent RAG workflow using LangGraph.

In this workflow we use two AI agents:
- The ‘Retriever’ one which is performing a semantic search (using the MCP tool)
- The ‘Answer’ one which is generating a final answer based on the documents found by the Retriever.
### Ray_serve_app.py
Script where we define Ray Serve deployment which serves the RAG workflow as a Rest API.

Ray Serve is used here to specify how this Rest API will be deployed, how to run proxy and worker processes which will listen for and handle requests, for example:
- How many resources (CPU, GPU) we will assign to it
- How many replicas we will create (each replica is a copy of our app handling requests)

How Rest API will be deployed is also partially configured in the ‘Ray Service’ Helm chart.

Fast API is used to define Rest API endpoints (a logic for how to handle requests).

This script uses the RAGWorkflow class from the rag_workflow.py script.

It doesn’t run proxy and worker processes. It only specifies:
- Logic for how to handle requests (using FastAPI)
- Ray Serve deployment configuration (how to run proxy and worker processes)

The actual processes (proxy and workers) that listen for and handle requests are started by the Kubernetes RayService CR which we configure and deploy using the ‘Ray Service’ Helm chart.

Environment variables used in the script:
- MCP_SERVER_URL – URL of the MCP server to use with a tool for semantic search which will be used by the agent.
### Ray_serve_app.zip
This is zipped ray_serve_app folder. It is used in the ‘Ray Service’ Helm chart (in the RayService CRD) to run our Ray Serve app on AKS.