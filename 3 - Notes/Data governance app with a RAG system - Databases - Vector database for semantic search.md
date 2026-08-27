Tags: [[__My_projects]]
#MyProjects 

# Introduction
We use Milvus as a vector database used to stored sentence embeddings used for the semantic search.

It is deployed using the `helm_charts/create_milvus_collection` Helm chart which runs Milvus and prepares a collection for embeddings in it.
## Milvus collection preparation
Helm chart which deploys Milvus, also runs the script from the `services/semantic_search/create_milvus_collection` folder to prepare a Milvus collection with specific fields where we will store embeddings and set up an index.
# Embedding ingestion pipeline
Pipeline ingesting embeddings into this vector database that will be used for a semantic search is described here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline]].