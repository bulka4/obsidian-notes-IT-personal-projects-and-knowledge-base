Tags: [[__My_projects]]
#MyProjects 

# Embeddings data inconsistency
We might encounter data inconsistency when a table description gets updated and the embedding ingestion pipeline fails. Then, embeddings used for semantic search are not up to date so semantic search uses old documentation.

To deal with this, we could save information about document and embedding versions. Each time a document gets updated we increase its version number. When a version number for embeddings is smaller than for a corresponding document, that means that embeddings are not up to date.

So in the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]) we would save information:
```
{
	tableID: ...
	version: ...
	description: ...
}
```

and in the vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]]) we would save similarly:
```
{
	vector: ...
	object_id: ... # Corresponding to the tableID
	version: ...
}
```

When embeddings are not up to date, we could for example show in the Data Governance UI ([[Data governance app with a RAG system - Data governance backend|link]]) a warning that the new documentation has not been processed yet when using the semantic search engine and it will use the old documentation.