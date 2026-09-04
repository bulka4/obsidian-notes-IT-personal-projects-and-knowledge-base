Tags: [[__My_projects]]
#MyProjects 

# Introduction
We use Milvus as a vector database used to stored sentence embeddings used for the semantic search.

It is deployed using the `helm_charts/create_milvus_collection` Helm chart which runs Milvus and prepares a collection for embeddings in it.
# Data model
Data model used in the vector database for semantic search looks like that:
```
Collection: document_chunks

id | vector        | text_chunk              | metadata
---+---------------+-------------------------+-------------------------
1  | [0.1,0.2...]  | "SQL joins combine..."  | {
                                                object_id: 1,
                                                chunk_id: 1
                                              }
2  | [0.4,0.8...]  | "Indexes improve..."    | {
                                                object_id: 1,
                                                chunk_id: 2
                                              }
3  | [0.3,0.5...]  | "MongoDB stores..."    | {
                                                object_id: 2,
                                                chunk_id: 1
                                              }
```

where:
- we have one collection for all table documents for which we create embeddings
- each record in that collection corresponds to one text chunk
- metadata indicates which document (in the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]])) the text chunk belongs to. It includes:
	- `object_type` - 'table' or 'column'
	- `object_name` - name of the table or column
	- `object_id` - ID of the table document (taken from the database documentation database)
	- `chunk_id` - ID of the chunk that belongs to the document

Include this metadata to enable filtering.
## Milvus collection preparation
Helm chart which deploys Milvus, also runs the script from the `services/semantic_search/create_milvus_collection` folder to prepare a Milvus collection with specific fields where we will store embeddings and set up an index.
# Embedding ingestion pipeline
Pipeline ingesting embeddings into this vector database that will be used for a semantic search is described here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline]].