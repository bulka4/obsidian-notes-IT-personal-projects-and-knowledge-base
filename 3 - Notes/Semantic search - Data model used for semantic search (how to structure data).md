Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
When we use a vector database for a semantic search, we usually split text documents into chunks ([[Semantic search - Chunking|link]]) (a fixed-length sequence of tokens) and calculate embeddings for each text chunk.

Then, we can store this data in a vector database in the following format:
```
Collection: document_chunks

id | vector        | text_chunk              | metadata
---+---------------+-------------------------+-------------------------
1  | [0.1,0.2...]  | "SQL joins combine..."  | {
                                                document_id: 10,
                                                chunk_id: 1
                                              }
2  | [0.4,0.8...]  | "Indexes improve..."    | {
                                                document_id: 10,
                                                chunk_id: 2
                                              }
3  | [0.3,0.5...]  | "MongoDB stores..."    | {
                                                document_id: 20,
                                                chunk_id: 1
                                              }
```

where:
- we have one collection for all text documents for which we create embeddings
- each record in that collection corresponds to one text chunk
- metadata indicates which document that text chunk belongs to