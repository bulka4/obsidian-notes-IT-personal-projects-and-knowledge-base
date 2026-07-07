Tags: [[_Obsidian]] [[_Software_Engineering]]

# Streaming responses
Implement
```
Server Sent Events
or
WebSockets
```

instead of waiting for the entire answer and then showing it at once, show different parts of the answer one by one as they are generated.
# Conversation memory
[[Chatbots - Conversation memory]].

Store:
- sessions
- history
- summarization
# Authentication
- JWT
- OAuth
- API keys
- Role-based access
# Rate limiting
[[Backend Engineering - Rate limiting]] 
- Redis
- Token bucket
- Circuit breakers
# Evaluation pipeline
[[Evaluation pipeline for a RAG system]].

Automatically measure
- retrieval precision
- recall
- latency
- hallucination rate

Very valuable for production AI systems.
# Benchmarks
Measure ([[Backend Engineering - Latency and throughput|link]]):
```
P50 latency
P95 latency
P99 latency
Throughput
CPU, Memory, GPU utilization
```
# Multiple retrieval strategies
Instead of
```
Vector search
```
implement
```
BM25
↓
Hybrid search
↓
Reranking
↓
Vector search
```

That demonstrates understanding of retrieval systems.
# Python SDK
Create a Python SDK for using the RAG system:
```python
answer = client.rag.query(
    question="How does Spark work?",
    top_k=5
)
```
