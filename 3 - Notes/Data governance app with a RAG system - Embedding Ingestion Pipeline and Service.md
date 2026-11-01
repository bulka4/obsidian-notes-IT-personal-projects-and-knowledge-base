Tags: [[__My_projects]]
#MyProjects 

# Introduction
The embedding ingestion pipeline converts documents from the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]), converts them into embeddings and ingests them into a vector store.

The embedding ingestion service is a service that waits for messages to appear in a specific Kafka topic (emitted by the Data Governance Backed ([[Data governance app with a RAG system - Data governance backend|link]])) and then runs the pipeline.

Those embeddings are used for semantic search ([[Data governance app with a RAG system - Semantic search API|link]]).

The pipeline clears all the current embeddings and inserts new ones for all the source documentation.
# Deployment
## Dependencies
Before we deploy the embedding ingestion pipeline, we need the following dependencies:
- Deployed MongoDB used as a database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]):
	- From this database, the pipeline will read documents and convert them into embeddings.
  ```shell
  	# Execute below commands from the helm_charts/mongo_db folder
	helm dependency build
	helm -n semantic-search install mongo-db . &
  ```

Just deploying MongoDB should be enough to start the embedding ingestion service, so it can connect to MongoDB. 

However, the service will not be able to perform the ingestion since the MongoDB will be empty. Ingestion is triggered when a user saves a table description from the Data Governance UI ([[Data governance app with a RAG system - Data governance backend|link]]).

To populate MongoDB with database documentation data, run the metadata extraction pipeline (more info here - [[Data governance app with a RAG system - Metadata extraction pipeline|link]]).
## Deploying the embedding ingestion service
To deploy the embedding ingestion service:
- Install the Milvus Helm chart:
	- It will deploy Milvus and create a collection in Milvus that will be used to store embeddings.
	- In Milvus we will store vector embeddings.
    ```bash
	# Execute below commands from the helm_charts/create_milvus_collection folder
	helm dependency build
	helm -n semantic-search install milvus . &
    ```
- Install Kafka Helm chart:
	```shell
	# Execute below commands from the helm_charts/kafka folder
	helm dependency build
	helm -n semantic-search install kafka . &
	```
- Create a topic in Kafka, where data governance backend will be emitting messages and embedding ingestion service will read messages from:
  ```shell
  kubectl -n semantic-search exec -it kafka-controller-0 \
	  -- kafka-topics.sh \
		  --create --topic table-descriptions \
		  --bootstrap-server kafka:9092 \
		  --partitions 1 \
		  --replication-factor 1
  ```
- Install the embedding ingestion service Helm chart:
  ```bash
	# Execute below commands from the helm_charts/embedding_ingestion_service folder
	helm -n semantic-search install emb-ing . &
  ```
# How to run the pipeline
## Create table descriptions
To create table descriptions for which we can generate and ingest embeddings:
- access UI at the URL `localhost:8080`
- go to the `Data catalog` section
- select a table from the left-hand side panel
- create a description and click on `save`
## Pipeline Helm charts
There are two Helm charts we can use to run the pipeline:
- `embedding_ingestion_pipeline` - Run the pipeline once
- `embedding_ingestion_service` - Run the pipeline every time a message comes to a specific Kafka topic indicating that table description in the documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]) has been updated.
## Dependencies
In order to run both Helm charts, we need to prepare the following dependencies:
- Milvus collection - 
	- With a proper schema defined (like described in the `ONNXEmbeddingModel` section below in this document).
	- It can be prepared using the `helm_charts/create_milvus_collection` Helm chart ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]])
- Source documents
	- Stored in MongoDB, with a proper schema like described in the `MongoDocumentSource` section below in this document.
	- It can be prepared using Data Governance Backend UI ([[Data governance app with a RAG system - Data governance backend|link]]):
		- access UI at the URL `localhost:8080`
		- go to the `Data catalog` section
		- select a table from the left-hand side panel
		- create a description and click on `save`

In order to run the `embedding_ingestion_service` Helm chart, we need additionally:
- Kafka:
	```shell
	# Execute below commands from the helm_charts/kafka folder
	helm dependency build
	helm -n semantic-search install kafka . &
	```
# How the pipeline works
The pipeline:
- Reads a documentation from the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]])
- Converts it into embeddings
    - It uses for that a saved ONNX model or downloads a new model from Hugging Face if such a model is not saved yet
- Clears a Milvus collection and inserts new embeddings

Pipeline from the `embedding_ingestion_service` Helm chart:
- Waits for messages to appear in a specific Kafka topic
	- Those messages are emitted by the Data Governance Backend ([[Data governance app with a RAG system - Data governance backend|link]]) when a table description gets updated
- When a message appears, run the pipeline
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
# Error handling
Ideas for error handling, not implemented yet.
## Retries
For the embedding ingestion pipeline, in case of failures, we could use retries with backoff ([[Software Engineering - Fault tolerance - Retries with backoff|link]]) or circuit breakers ([[Software Engineering - Fault tolerance - Circuit breakers|link]]).
## Idempotency
We should make the embedding ingestion pipeline ([[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|link]]) idempotent as Kafka's messages can be processed twice (as described here - [[Kafka - Consumers - Processing a message multiple times|link]]).

To remind how this works:
- When a document, in the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]), gets updated in the Data Governance UI ([[Data governance app with a RAG system - Data governance backend|link]]), then Kafka's event is emitted describing which document was updated
- The embedding ingestion service looks for those Kafka's events about documents being updated and when such an event appears, it runs the ingestion pipeline

To avoid running the embedding ingestion pipeline twice when one a document is updated, we could:
- Store in the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]) info about when the last time each document was updated
- Store in the vector database with embeddings ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]]) info about when the last time embeddings for each document were updated

Then, we run the ingestion pipeline for a document only when the date of updating the document is earlier than the date of updating embeddings for this document.
## Embeddings data inconsistency
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

Another problem is when embeddings for some chunks for a document has been updated but not for all the chunks. This is covered in the embedding ingestion pipeline document > Error handling section > Atomicity ([[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service#Error handling|link]]).
### Atomicity
We should make sure that either all embeddings for all chunks for a document are updated or none, to avoid inconsistency, a situation when only a part of embeddings for one document is updated and we don't know which ones.
#### Problem with Milvus
Milvus unfortunately doesn't support creating atomic transactions, so we can't perform an update of all embeddings for all chunks for one document as a single transaction.

Also, we can't have multiple versions of embeddings in Milvus and information about the active version per document, something like:
```
embeddings table:
document_id | text_chunk | embedding  | version
1             'word'       [0.1, ...]   1
1             'word 2'     [0.2, ...]   2

active embedding version table:
document_id | active_embedding_version
1             1
```
 because, when performing semantic search, we couldn't figure out which version is the active one per document. 
 
 In order to do that, we would need to join the collection with embeddings with the collection about what is the active version for each document and we can't do that, something like:
 ```sql
 select * from
	 embeddings_table as e
	 -- inner join will filter out inactive embeddings
	 inner join active_embedding_version as av
		 on av.document_id = e.document_id
 ```
#### Possible solutions
What we could do is:
- Use a vector store that provides atomic transactions (e.g. pgvector)
- Use a vector store that provides joins so we could use another table indicating what is the active embedding version per document (e.g. pgvector)
- Use this updating pattern (it is still non atomic but better):
	- In the Milvus collection, add the `valid` field indicating whether or not a record is valid (invalid records are not used in search)
	- When creating new embeddings for a document, create new invalid records, leaving old valid records
	- Once all the new embeddings have been prepared, mark them as valid and remove old records for this document
  
  This is still non atomic but now replacing old embeddings with a new ones is done only by marking new ones as valid as removing old records which is much quicker than generating embeddings and inserting them.
## Dead-letter-queue (DLQ)
When the embedding ingestion pipeline fails too many times, it could send a DLQ message to a separate Kafka's topic (just for DLQ messages) containing info about the pipeline that we tried to execute and error, for example:
```json
{
  "original_topic": "document-updated",
  "original_partition": 3,
  "original_offset": 1842,
  "document_id": 42,
  "version": 7,
  "error": "Embedding model unavailable",
  "failed_at": "..."
}
```

we could use later this info for another retry, automatic or manual if needed.
## Out of order Kafka messages
When Kafka messages are stored in different partitions, they can be processed by a consumer in a different order than they were generated ([[Kafka - Out of order messages|link]]).

So we might have messages about updating a single document like this:
```
Document v1
Document v2
Document v3
```

but they are processed in a different order, e.g.:
```
Document v1
Document v3
Document v2
```

and then we end up with embeddings for the `v2` version.

To handle this, we could store in the documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]) and in the vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]]) info about a version of documents and embeddings:
```
MongoDB - database documentation database
document_id = A
version = 12

Milvus - Vector store
document_id = A
version = 11
embedding = ...
```

When performing an embedding ingestion, we could check:
- what is the version of the document for which we are performing the ingestion
- what is the latest version of that document available in the documentation database

If the version from the first step is smaller than from the second step, then don't perform the ingestion.
# Improvements
## Incremental ingestion
To make this ingestion incremental we would need to:
- Change the Data Governance Backend ([[Data governance app with a RAG system - Data governance backend|link]]) to save information about when each document has been modified the last time
- Save in the Milvus vector database information about when each record has been inserted
- Go through all the documents created by the Data Governance Backend and insert into the Milvus vector database embeddings only for those documents for which the inserted date from Milvus is smaller than the last modified date from the Data Governance Backend