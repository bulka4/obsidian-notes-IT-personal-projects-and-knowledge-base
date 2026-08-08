Tags: [[__My_projects]]
#MyProjects 

# Introduction
RAG system is an API deployed using Ray Serve that exposes an endpoint for getting responses to questions:
- It is used by the data governance backend ([[Data governance app with a RAG system - Data governance backend|link]])
- It uses the semantic search engine service ([[Data governance app with a RAG system - Semantic search service|link]])
# Architecture overview
Here are the most important components of this RAG system:
- Multi-agent workflow created using LangGraph
- MCP server providing a tool for semantic search
- Vector database used for storing document embeddings
- FastAPI + Ray Serve to serve it as Rest API