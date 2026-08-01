Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
Versioning embeddings means keeping track of which embedding model and configuration were used to create each vector.

This matters because embeddings are not permanent representations. If you change the embedding model, the same text can produce a different vector.

A common approach is to store metadata telling us how each embedding was created:
```json
{
  "document_id": 123,
  "chunk_id": 5,
  "text": "How do SQL indexes work?",
  "embedding_model": "model-v2",
  "embedding_version": 2,
  "created_at": "2026-08-01"
}
```
# Why is this useful
## 1. Migrating embedding models
We may want to move from one model to another for creating embeddings. We can keep temporarily both embedding versions and compare search quality before switching.
## 2.Reproducibility
If someone asks:
> "Why did this document appear in search results?"

you can know:
- which embedding model was used,
- when it was generated,
- what chunking strategy created the chunk.
