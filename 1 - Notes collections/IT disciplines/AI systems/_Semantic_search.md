Tags: [[_Semantic_search]] [[__AI_systems]]
#SemanticSearch #AISystems 

# Introduction
1. [[Semantic search - How it works & embeddings]]
2. [[Semantic search - Vector databases]]
3. [[Semantic search - Data model used for semantic search (how to structure data)]]
4. [[Semantic search - Chunking]]
	1. [[Semantic search - Chunking metadata]]
	2. [[Semantic search - Overlapping chunks]]
	3. [[Semantic search - Chunking strategies]]
5. [[Semantic search - Meta]]
# Other topics to explore
1. **Semantic search - Overview**
    - keyword search vs semantic search
    - embeddings as meaning representation
    - search pipeline
2. **Semantic search - Data model**
    - documents
    - chunks
    - metadata
    - document IDs
    - linking chunks back to sources
3. **Semantic search - Embedding generation**
    - embedding models
    - model choice
    - embedding dimensions
    - domain-specific embeddings
    - changing embedding models
4. **Semantic search - Chunking**
    - chunk size
    - overlap
    - chunking strategies
    - metadata
    - semantic chunking
5. **Semantic search - Query processing**
    - query embedding
    - query rewriting
    - query expansion
    - handling short queries
6. **Semantic search - Retrieval strategies**
    - top-k retrieval
    - similarity thresholds
    - hybrid search
    - multi-vector retrieval
7. **Semantic search - Hybrid search**
    - combining:
        - keyword search (BM25)
        - vector search
    - ranking results from both
8. **Semantic search - Reranking**
    - why vector similarity is not enough
    - cross-encoder rerankers
    - two-stage retrieval:
        - retrieve many candidates
        - rerank best candidates
9. **Semantic search - Evaluation**
    - precision/recall
    - MRR
    - NDCG
    - retrieval quality evaluation
    - creating test datasets
10. **Semantic search - Production architecture**

- document ingestion pipeline
- embedding pipeline
- vector database
- search API
- caching
- monitoring

11. **Semantic search - Common failure modes**

- bad chunking
- wrong embedding model
- missing metadata
- irrelevant retrieval
- stale embeddings