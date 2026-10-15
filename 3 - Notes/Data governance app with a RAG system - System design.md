Tags: [[__My_projects]]
#MyProjects 

# System architecture diagram
System architecture diagram (arrows indicates that one service uses / communicates with another):
![a](system_architecture_diagram.svg)
# Workflow/application orchestration
Workflow/application orchestration is implemented in the `RAGWorkflow` class, defined in the `services/semantic_search/routes/RAGWorkflow.py` file.
# Entities
We have one entity which is a document. It is:
- Created in the Data Governance UI
- Stored in a database
- It has created embeddings stored in a vector store for semantic search
# Use cases
- Semantic search 
	- used to search through documents (entities)
	- defined in the `services/semantic_search/routes/routes.py` script
	- exposed as the `GET /search` route
	- implemented as the `RAGService.search` function (the `routes.py` file)
	- converts the query into an embedding and retrieves documents with similar embeddings from a vector store
- answering a question using the RAG system
	- retrieves documents (entities) relevant to the question using semantic search and answers a question based on them
	- defined in the `services/semantic_search/routes/routes.py` script
	- exposed as the `POST /ask` route
	- implemented as the `RAGWorkflow.answer` function from the RAG workflow (the `RAGWorkflow.py` file)
# Interfaces / abstractions
Interfaces / abstractions from the `services/semantic_search/routes/interfaces.py` script that defines adapters (described further in the "Adapters" section):
- `EmbeddingModel` - For generating embeddings using LLM
- `VectorStore` - For finding embeddings in a vector store for semantic search
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
We use the following outbound adapters which are used by use cases for interacting with external technologies:
- defined in the `semantic_search/routes` folder (the REST API server):
	- The `MilvusVectorStore.search` function for retrieving vectors from the Milvus vector store (implementation of the `VectorStore` interface)
	- The `TransformersEmbeddingModel.run` function for generating embeddings using a LLM and the `transformers` library (implementation of the `EmbeddingModel` interface)
	- The `MCPSemanticSearchTool.search` function for calling a MCP tool for semantic search (implementation of the `SemanticSearchTool` interface)
	- The `TransformersAnswerModel.generate` function for generating an answer using a LLM and the `transformers` library (implementation of the `AnswerModel` interface)
- defined in the `semantic_search/mcp_server` folder (the MCP server):
	- The `search_docs` function for calling the Semantic search API
## Inbound adapters (API routes)
We use the following inbound adapters (`FastAPI` routes) which takes HTTP requests and calls uses cases which prepares a response:
- The `GET /search` route - for performing semantic search
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
# API contracts
## Defining request and response schemas using data classes
We use data classes to define what fields are expected in the request for a REST API route and what fields are in the response:
```python
# A result of searching through a vector store
@dataclass
class SearchResult:
    # ID of the document (taken from the database documentation database)
    object_id: int
    # One text chunk from the document          
    text_chunk: str
    # Similarity score for this text chunk and the given query
    similarity_score: float

@dataclass
class AskRequest:
    query: str
    top_k: int = 3

@dataclass
class AskResponse:
    answer: str
    retrieved_docs: list[SearchResult]

@app.post("/ask", response_model=AskResponse)
async def ask(self, request: AskRequest) -> AskResponse:
	...
```
## More info
More info about contracts - [[Software Engineering - Architecture concepts - API contracts]].
# CQRS
We implement CQRS by grouping functions and data models by writes (commands) and reads (queries).
## Writes (commands)
### Functions
For writes (commands) we use functions:
#### Embedding ingestion service
For the embedding ingestion service (the `services/semantic_search/embedding_ingestion_service` folder):
- `MilvusVectorStore.insert()` - insert embeddings into the Milvus vector store
### Data models
For writes (commands) we have data models:
- MongoDB database documentation ([[Data governance app with a RAG system - Databases - Database documentation|link]]) - database with database documentation (this is the source of truth about documents)
## Reads (queries)
For reads (queries) we use functions:
### Functions
#### Semantic search
For routes related to semantic search (the `services/semantic_search/routes` folder):
- `MilvusVectorStore.search()` - search embeddings in the Milvus vector store
#### Embedding ingestion service
For the embedding ingestion service (the `services/semantic_search/embedding_ingestion_service` folder):
- `MongoDocumentSource.read_chunks()` - read text chunks for which we will prepare embeddings
- `KafkaMessageConsumer.consume()` - look for messages from Kafka and yield them
### Data models
For reads (queries) we have data models:
- Milvus vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]]) - storing vector embeddings for semantic search (those embeddings are created based on the documents from the MongoDB database documentation ([[Data governance app with a RAG system - Databases - Database documentation|link]]))
# Data consistency
We use the eventual consistency model. When a new document appears, embeddings for it might be temporarily outdated. This data inconsistency is described more here - [[Data governance app with a RAG system - Error handling]].