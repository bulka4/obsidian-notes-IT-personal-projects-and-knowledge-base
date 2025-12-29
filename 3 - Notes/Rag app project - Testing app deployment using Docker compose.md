Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes how to test deployment of the RAG app from this project - [[RAG app project|link]], using Docker compose.

Before deploying on AKS, we can run our app with RAG workflow locally for testing using Docker Compose, the docker-compose-rag.yml file.

I am not sure if it works correctly at this moment. It did work before, it was used for testing, but after that I made some changes in code and it might require some modifications to be used again.

We are running there a few services:
- rag – It contains all the elements needed for running an agent:
    - Mcp_server/mcp_server.py – Script running a MCP Server with a tool for semantic search
    - Prepare_milvus_db /prepare_milvus_db.py script – Script preparing a sample data in Milvus db (documents with their embeddings)
    - Ray_serve_app/rag_workflow.py – Script with a class running a RAG LangGraph workflow.
- etcd – Service running etcd used by the Milvus db.
- minio - Service running MinIO used by the Milvus db.
- milvus – Service running Miluvs db.

We can’t run the Ray Serve app in Docker compose as that require Ray cluster. We could run Ray in a standalone mode in a container to test Ray Serve app but we didn’t do this in this repo.

We are using the official Docker Compose described on the Milvus website: [milvus.io/docs](https://milvus.io/docs/install_standalone-docker-compose.md). There is a link for downloading this Docker Compose file: [github.com/milvus-io](https://github.com/milvus-io/milvus/releases/download/v2.6.0/milvus-standalone-docker-compose.yml).

These 3 services from the Docker Compose file: etcd, minio and milvus, where originally contained in this file. The agent service was added by us.