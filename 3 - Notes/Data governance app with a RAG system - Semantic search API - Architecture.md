Tags: [[__My_projects]]
#MyProjects 

# Workflow/application orchestration
Workflow/application orchestration is implemented in the `RAGWorkflow` class, defined in the `services/semantic_search/routes/RAGWorkflow.py` file.
# Use cases
Semantic search use cases that is used in the `services/semantic_search/routes/routes.py` script:
- Implemented as the `RAGService.search` function (the `routes.py` file)
- It converts the query into an embedding and retrieves documents with similar embeddings from a vector store

It is a function assigned to `FastAPI` route `/search`.
# Interfaces / abstractions
Interfaces / abstractions from the `services/semantic_search/routes/interfaces.py` script that are used as adapters:
- `EmbeddingModel` - For generating embeddings using LLM
- `VectorStore` - For finding embeddings in a vector store for semantic search

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
We use the following outbound adapters which are used by use cases for interacting with external technologies:
- defined in the `semantic_search/routes` folder (the REST API server):
	- The `MilvusVectorStore.search` function for retrieving vectors from the Milvus vector store (implementation of the `VectorStore` interface)
	- The `TransformersEmbeddingModel.run` function for generating embeddings using a LLM and the `transformers` library (implementation of the `EmbeddingModel` interface)
- defined in the `semantic_search/mcp_server` folder (the MCP server):
	- The `search_docs` function for calling the Semantic search API
## Inbound adapters (API routes)
We use the following inbound adapters (`FastAPI` routes) which takes HTTP requests and calls uses cases which prepares a response:
- The `GET /search` route - for performing semantic search
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