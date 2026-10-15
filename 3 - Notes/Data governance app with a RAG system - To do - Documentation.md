Tags: [[__My_projects]]
#MyProjects 

# Introduction
New documents to prepare:
- [[Data governance app with a RAG system - Error handling]]
- [[Data governance app with a RAG system - System architecture]]
- [[Data governance app with a RAG system - System design]]
# Topics to explore
Topics to explore:
- event driven architecture
	- backpressure
# How to organize the documentation
I could organize the documentation like this:
```
Architecture
├── System architecture
├── Workflow / orchestration
├── Entities
├── Use cases
├── Interfaces / abstractions
├── Adapters
├── CQRS
└── Event-driven architecture

Data
├── Data stores
├── Data consistency
├── Data versioning
├── Idempotency
└── Data reconciliation

APIs
├── API contracts
├── API versioning
├── OpenAPI
└── Contract testing

Reliability
├── Error handling
├── Retries
├── Timeouts
├── Circuit breakers
├── DLQ
└── Graceful degradation

RAG / ML
├── Embeddings
├── Embedding model versioning
├── Chunking
├── Retrieval
├── Reranking
├── RAG evaluation
└── Prompt injection / AI security

Observability
├── Metrics
├── Logs
├── Tracing
├── Correlation IDs
└── Alerting

Infrastructure
├── Configuration
├── Secrets
├── Kubernetes
├── Scaling
├── Deployment strategy
└── Infrastructure vs application state

Security
├── Authentication
├── Authorization
├── Network security
├── Secrets
└── Data protection
```
# Questions
# ChatGPT prompt
I have a project where:
- users can create a database documentation
- there is a semantic search engine and rag system
- when a document is updated, a kafka's event is emitted and a pipeline ingests embeddings for it into a vector store
- it is built using nodejs, langgraph, milvus, kubernetes, kafka