Tags: [[_My_projects]]
#MyProjects 

# Introduction
In the RAG app project ([[RAG app project|link]]), we have the following Dockerfiles:
- Semantic search
    - Saved as apps/docker_images/semantic.search.Dockerfile.
    - Used for building an image where we can perform semantic search (interact with Milvus db and create sentence embeddings).
    - Used as a base image for building images for MCP Server and preparing Milvus db.
- MCP Server
    - Saved as apps/mcp_server/Dockerfile.
    - Used for building an image for MCP Server.
    - Uses the Semantic Search image as a base one.
- Preparing Milvus db
    - Saved as apps/prepare_milvus_db/Dockerfile.
    - Used for building an image for running a script which prepares a collection and sample data in Milvus db.
    - Uses the Semantic Search image as a base one.
- Ray Serve app
    - Saved as apps/ray_serve_app/Dockerfile.
    - Used for building an image for running a Ray Serve app which creates a Rest API serving a RAG LangGraph workflow.

Dockerfiles for MCP and Peparing Milvus db will be created by Terrafom as described in the ‘Terraform section’. Terraform will insert into them proper values about created Azure resources.