Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
When creating chunks ([[Semantic search - Chunking|link]]), we usually save them with additional metadata such as:
```json
{
  "chunk_id": "doc123_chunk5",
  "document_id": "doc123",
  "text": "...", // chunk text
  "page": 12,
  "section": "Replication",
  "embedding": [...]
}
```

so we know:
- What is the chunk's text
- What is its embedding (used for a semantic search)
- Which document does it comes from (so we can find this document and show it in results of a semantic search)