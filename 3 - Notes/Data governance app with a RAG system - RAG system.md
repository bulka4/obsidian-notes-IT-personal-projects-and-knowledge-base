Tags: [[__My_projects]]
#MyProjects 

# Introduction
RAG system is a Ray Serve app that exposes an endpoint for asking questions. It is used by the data governance app.
# Architecture overview
Here are the most important components of this RAG system:
- Multi-agent workflow created using LangGraph
- MCP server providing a tool for semantic search
- Vector database used for storing document embeddings
- FastAPI + Ray Serve to serve it as Rest API