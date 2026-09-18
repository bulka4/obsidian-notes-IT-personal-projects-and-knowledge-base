Tags: [[__My_projects]]
#MyProjects 

# Introduction
New documents to prepare:
- [[Data governance app with a RAG system - Program design]]
- [[Data governance app with a RAG system - Error handling]]
- [[Data governance app with a RAG system - Further development]]
# Topics to explore
Topics to explore:
- What architecture to use (e.g. layered, hexagonal)
- Separate application state from infrastructure state
- CQRS
	- separate reads (saving documentation and embeddings) and writes (semantic search, generating answers)
	- use different databases
	- scale separately
- api versioning

Error handling topics to explore:
- Observability
    - Metrics such as:
        - ingestion success/failure rate
        - ingestion duration
        - number of documents waiting for embeddings
        - number of stale documents
        - embedding generation latency
        - semantic-search latency
    - Logs/traces could let you follow a document through the system.
- Backpressure / queueing
    - If users suddenly update thousands of documents, don't necessarily process everything immediately.
    - Put embedding jobs into a queue and process them asynchronously with controlled concurrency.
- idempotent embedding ingestion
	- Why it should be idempotent? Because Kafka's message can be processed twice?
- Atomic embedding ingestions
	- Either all embeddings for all chunks for a document are updated or none
	- For a document, we don't want to have only a part of chunks to have updated embeddings
- Dead-letter
	- After a certain number of ingestion failures, put the document/job into a failed state rather than retrying forever.
    - Keep the error information for debugging.
- retries of embedding ingestion (e.g. with exponential backoff)
# Questions
- 