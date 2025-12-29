Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes architecture 
# LangGraph multi-agent workflow
LangGraph is used to create a multi-agent workflow with two AI agents:
- The ‘Retriever’ one which is performing a semantic search (using the MCP tool)
- The ‘Answer’ one which is generating a final answer based on the documents found by the Retriever.
# Milvus
Milvus is used as a vector database for storing vector embeddings of documents used for semantic search.

User's question is converted into a vector embedding and in Milvus we find documents with the most similar embeddings.
# MCP
MCP server provides a tool for performing semantic search. This tool is used by the 'Retriever' agent from the LangGraph workflow.
# FastAPI
FastAPI is used to define Rest API endpoints which clients can use to ask a question to our RAG system.

It parses clients' HTTP requests and prepares a response.
# Ray Serve
Ray Serve is used to:
- Running a proxy which listens to clients' requests
- Enabling distributed execution of Rest API endpoints - i.e. execute different endpoint's tasks in parallel across multiple servers
- Optimizing request handling, using for example:
	- Request batching - Multiple requests are combined into a single forward pass
	- Fractional GPUs utilization
		- Multiple processes handling requests can be ran on a single GPU what gives better GPU utilization