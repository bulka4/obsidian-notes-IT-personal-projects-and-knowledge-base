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
# Improvements
## Incremental ingestion
To make this ingestion incremental we would need to:
- Change the Data Governance Backend ([[Data governance app with a RAG system - Data governance backend|link]]) to save information about when each document has been modified the last time
- Save in the Milvus vector database information about when each record has been inserted
- Go through all the documents created by the Data Governance Backend and insert into the Milvus vector database embeddings only for those documents for which the inserted date from Milvus is smaller than the last modified date from the Data Governance Backend