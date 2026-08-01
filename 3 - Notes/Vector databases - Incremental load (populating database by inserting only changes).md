Tags: [[_Databases]] [[_Vector_databases]]
#Databases #VectorDatabases 

# Introduction
To apply incremental load, i.e. populate a vector database by inserting embeddings only for documents that has changed, we can use the following technique:
- Get information about which documents has been created, modified and deleted
- For new documents, insert their embeddings
- For deleted documents, delete their embeddings
- For modified documents, delete their embeddings and insert new embeddings, for the new version of the document
# Replacing all chunks vs only changed ones
When a document gets modified, we can:
- replace embeddings for all the old chunks
- or replace embeddings only for the changed chunks
# Metadata
To apply incremental load, we need to have metadata telling us when the last time each document and embedding were modified.