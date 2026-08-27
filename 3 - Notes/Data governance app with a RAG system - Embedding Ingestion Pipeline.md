Tags: [[__My_projects]]
#MyProjects 

# Introduction
Embedding ingestion pipeline is a scheduled pipeline ingesting vector embeddings into the vector database used for the semantic search ([[Data governance app with a RAG system - Semantic search service|link]]). It clears all the current embeddings and inserts new ones for all the source documentation.

Those embeddings are created based on the SQL server documentation created by users.

This pipeline is:
- programmed in Python
- scheduled using a CronJob
	- It could be also scheduled in Airflow but for this project Airflow is not needed
# How to run the pipeline (dependencies)
In order to run this pipeline, we need to prepare the following dependencies:
- Milvus collection - 
	- With a proper schema defined (like described in the `ONNXEmbeddingModel` section below in this document).
	- It can be prepared using the `helm_charts/create_milvus_collection` Helm chart ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]])
- Source documents
	- Stored in MongoDB, with a proper schema like described in the `MongoDocumentSource` section below in this document.
	- It can be prepared using Data Governance Backend UI ([[Data governance app with a RAG system - Data governance backend|link]])
# How the script works
The main.py script:
- Reads a documentation from the MongoDB database (all documents from a specific database and collection)
- Converts it into embeddings
    - It uses for that a saved ONNX model or downloads a new model from Hugging Face if such a model is not saved yet
- Clears a Milvus collection and inserts new embeddings
## `MongoDocumentSource`
The `document_source/MongoDocumentSource.py` script contains the `MongoDocumentSource` class used to prepare text chunks from which we can create vector embeddings.

We assume there that the documentation in MongoDB is about tables and columns and has following schema:
```
    col_doc_schema:
        {
            columnName: String
            ,foreignKey: Boolean
            ,primaryKey: Boolean
            ,columnDescription: String
            ,columnDescriptionEncoded: Array
        }

    table_doc_schema:
        {
            tableId: Number
            ,tableName: String
            ,sourceScript: String
            ,tableDescription: String
            ,tableDescriptionEncoded: Array
            ,columns: [col_doc_schema]
        }
```
## `ONNXEmbeddingModel`
Using the `ONNXEmbeddingModel` class from the `embedding_model/ONNXEmbeddingModel.py` script we can download a new model from Hugging Face and save it in the ONNX format or load already saved ONNX model and load this model to be ready to use.
## `MilvusVectorStore`
Using the `MilvusVectorStore` class from the `vector_store/MilvusVectorStore.py` script we can insert vector embeddings into a collection with the following fields:
- id: INT64
- embedding: FLOAT_VECTOR
- text: VARCHAR
- metadata: JSON

Before inserting embeddings, all the current embeddings in the collection are removed.

Embeddings are generated using the `ONNXEmbeddingModel` class.
# Improvements
## Incremental ingestion
To make this ingestion incremental we would need to:
- Change the Data Governance Backend ([[Data governance app with a RAG system - Data governance backend|link]]) to save information about when each document has been modified the last time
- Save in the Milvus vector database information about when each record has been inserted
- Go through all the documents created by the Data Governance Backend and insert into the Milvus vector database embeddings only for those documents for which the inserted date from Milvus is smaller than the last modified date from the Data Governance Backend