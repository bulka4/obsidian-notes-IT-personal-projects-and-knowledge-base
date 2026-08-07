Tags: [[__My_projects]]
#MyProjects 

# Introduction
There is a separate service providing a semantic search engine.
# Serving
Semantic search engine will be served as:
- REST API endpoint
- MCP tool - which calls that REST API endpoint

MCP tool will be used by the RAG system and REST API endpoint by the data governance app directly.
# Clients
Clients that use this engine:
- RAG system 
- searching option (displaying relevant documents to a user)
# Data model
Data model used in a vector database for semantic search looks like that:
```
Collection: document_chunks

id | vector        | text_chunk              | metadata
---+---------------+-------------------------+-------------------------
1  | [0.1,0.2...]  | "SQL joins combine..."  | {
                                                document_id: 1,
                                                chunk_id: 1
                                              }
2  | [0.4,0.8...]  | "Indexes improve..."    | {
                                                document_id: 1,
                                                chunk_id: 2
                                              }
3  | [0.3,0.5...]  | "MongoDB stores..."    | {
                                                document_id: 2,
                                                chunk_id: 1
                                              }
```

where:
- we have one collection for all text documents for which we create embeddings
- each record in that collection corresponds to one text chunk
- metadata indicates which document that text chunk belongs to

Metadata to include:
- `database`
- `schema`
- `object_type` - table or column
- `object_name` - table or column name
- `object_id` 
- `chunk_id`

Include this metadata to enable filtering.
# Data pipeline populating a vector database
Data pipeline populating a vector database works like this:
- Data is ingested using Python
- Scheduled using a CronJob