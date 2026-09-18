Tags: [[__My_projects]]
#MyProjects 

# Overview
Here are the most important components of this RAG system:
- Multi-agent workflow created using LangGraph
- MCP server providing a tool for semantic search
- Vector database used for storing document embeddings
- FastAPI + Ray Serve to serve it as Rest API
# Workflow/application orchestration
Workflow/application orchestration is implemented in the `RAGWorkflow` class, defined in the `services/semantic_search/routes/RAGWorkflow.py` file.
# Use cases
Use case for answering a question using the RAG system that is used in the `services/semantic_search/routes/routes.py` script:
- Implemented as the `RAGWorkflow.answer` function from the RAG workflow (the `RAGWorkflow.py` file)
- It retrieves documents relevant to the question using semantic search and answers a question based on them

It is a function assigned to `FastAPI` routes `/ask`.
# Interfaces / abstractions
Interfaces / abstractions from the `services/semantic_search/routes/interfaces.py` script that are used as adapters:
- `SemanticSearchTool` - A tool for semantic search (implemented using e.g. MCP)
- `AnswerModel` - For generating an answer using LLM

Their specific implementations are described further in this document in the "Adapters" section.
# Data classes (data transfer objects)
We use data classes to create objects for holding data:
- `SearchResult` - holds a result of semantic search (searching through a vector store). It contains the fields:
	- `object_id` - ID of the document (taken from the database documentation database)
	- `text_chunk` - One text chunk from the document
	- `similarity_score` - Similarity score for this text chunk and the given query
- `RAGState` - holds a `LangGraph` workflow state (containing graph input parameters, documents retrieved using semantic search and generated answer). It contains the fields:
	- `query`
	- `top_k`
	- `retrieved_docs`
	- `answer`
- `AskRequest` - holds input parameters for the use case for generating an answer using the RAG system. It contains the fields:
	- `query`
	- `top_k`
- `AskResponse` - holds the output of the use case for generating an answer using the RAG system It contains the fields:
	- `answer`
	- `retrieved_docs`
# Adapters
## Outbound adapters
We use the following outbound adapters (defined in the `semantic_search/routes` folder) which are used by use cases for interacting with external technologies:
- The `MCPSemanticSearchTool.search` function for calling a MCP tool for semantic search (implementation of the `SemanticSearchTool` interface)
- The `TransformersAnswerModel.generate` function for generating an answer using a LLM and the `transformers` library (implementation of the `AnswerModel` interface)
## Inbound adapters (API routes)
We use the following inbound adapters (`FastAPI` routes) which takes HTTP requests and calls uses cases which prepares a response:
- The `POST /ask` route - for generating answers using the RAG system
# Frameworks and drivers
Frameworks and drivers we use:
- Milvus
- Kafka
- MongoDB
- FastAPI
- Redis
- Kubernetes
# Configuration
Configuration is done through environment variables and it defines e.g. from where to load a model or which Milvus server to connect to.