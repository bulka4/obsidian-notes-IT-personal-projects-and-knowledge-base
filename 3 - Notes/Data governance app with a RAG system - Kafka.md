Tags: [[__My_projects]]
#MyProjects 

# Introduction
Kafka is used in the embedding ingestion pipeline, run using the `helm_charts/embedding_ingestion_service` Helm chart.
# Deployment
To deploy it, install the Helm chart:
```shell
# Execute below commands from the helm_charts/kafka folder
helm dependency build
helm -n semantic-search install kafka . &
```

then Kafka can be reached using the `kafka:9092` hostname.
## Prepare a topic
Create a topic in Kafka, where data governance backend will be emitting messages and embedding ingestion service will read messages from:
  ```shell
  kubectl -n semantic-search exec -it kafka-controller-0 \
	  -- kafka-topics.sh \
		  --create --topic table-descriptions \
		  --bootstrap-server kafka:9092 \
		  --partitions 1 \
		  --replication-factor 1
  ```
# Emitting messages
The data governance backend ([[Data governance app with a RAG system - Data governance backend|link]]) emits messages to Kafka when a table description is updated. 

We use for that a function defined in the `modules/kafka_producer.js` script which is used in the route for updating table descriptions, defined in the `routes/table_docs_route.js` script.
# Processing messages
Messages are processed by the embedding ingestion service ([[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|link]]) which runs an embedding ingestion pipeline when a message appears indicating that a table description has been updated.

The pipeline then converts new table descriptions into embeddings and inserts them into a vector store. It does it for all the descriptions always (full truncate and load).
# Kafka debugging
- Check available messages in a topic:
	```shell
	kubectl -n semantic-search exec -it kafka-controller-0 \
		-- kafka-console-consumer.sh \
		--bootstrap-server kafka:9092 \
		--topic table-descriptions \
		--from-beginning
	```
- Produce a message using Kafka:
  ```shell
	kubectl -n semantic-search exec -it kafka-controller-0 -- \
	  kafka-console-producer.sh \
	  --bootstrap-server localhost:9092 \
	  --topic table-descriptions
	  
	# Enter the below value
	hello
  ```