Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
In vector databases, **caching** means keeping frequently accessed data in faster storage (usually RAM) to reduce latency.

Common things that can be cached:
1. Vectors
    - Frequently searched embeddings kept in memory instead of reading from disk.
2. Index structures
    - Parts of HNSW/IVF indexes kept in RAM for faster traversal.
3. Query results
    - If the same or very similar query is repeated, return a cached result instead of running vector search again.