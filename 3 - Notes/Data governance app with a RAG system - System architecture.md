Tags: [[__My_projects]]
#MyProjects 

# System architecture diagram
System architecture diagram (arrows indicates that one service uses / communicates with another):
![a](system_architecture_diagram.svg)

# System components
System consists of the following parts:
## Source MS SQL Server
We deploy on Kubernetes the MS SQL Server from which we collect metadata and for which we create documentation in the data governance app.

More information is here - [[Data governance app with a RAG system - Source MS SQL Server]].
## Metadata extraction pipeline
Extracting and saving metadata from the source SQL server (info about tables, columns, sql scripts from views, jobs etc.)

More information:
- [[Data governance app with a RAG system - Metadata extraction pipeline]]
	- [[Data governance app with a RAG system - Metadata extraction - New code architecture|New code architecture]] 
## Databases
- [[Data governance app with a RAG system - Databases]]
	- [[Data governance app with a RAG system - Databases - Database documentation|Database documentation]] 
	- [[Data governance app with a RAG system - Databases - Data lineage data|Data lineage data]] 
	- [[Data governance app with a RAG system - Databases - Vector database for semantic search|Vector database for semantic search]] 
	- [[Data governance app with a RAG system - Databases - Redis for caching|Redis for caching]] 
## Data governance backend
- Serving UI
- Handling authentication and authorization

More information:
- [[Data governance app with a RAG system - Data governance backend]]
	- [[Data governance app with a RAG system - Data governance backend#Architecture|Architecture]] 
		- [[Data governance app with a RAG system - Data governance backend#HTTP server and routes|HTTP server and routes]] 
		- [[Data governance app with a RAG system - Data governance backend#Databases and data models|Databases and data models]] 
			- [[Data governance app with a RAG system - Databases - Database documentation|Database documentation]] 
			- [[Data governance app with a RAG system - Databases - Data lineage data|Data lineage data]] 
		- [[Data governance app with a RAG system - Data governance backend#Authentication and authorization|Authentication and authorization]] 
		- [[Data governance app with a RAG system - Data governance backend#Caching - Redis|Caching - Redis]] 
	- [[Data governance app with a RAG system - Data governance backend#Features|Features]] 
		- [[Data governance app with a RAG system - Data governance backend#Data lineage visualizations|Data lineage visualizations]] 
	- [[Data governance app with a RAG system - Data governance backend#Kubernetes deployment|Kubernetes deployment]] 
## Semantic search service
- Providing semantic search functionality

More information:
- [[Data governance app with a RAG system - Semantic search API]]
	- [[Data governance app with a RAG system - Semantic search API - Running and using the REST API server|Running and using the REST API server]] 
	- [[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|Embedding Ingestion Pipeline]] 
	- [[Data governance app with a RAG system - Databases - Vector database for semantic search|Vector database for semantic search]] 
	- [[Data governance app with a RAG system - Ray Serve]]
## Embedding Ingestion Pipeline
- Ingesting vector embeddings into the vector database using SQL database documentation created by users

More information:
- [[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service]]
	- [[Data governance app with a RAG system - Databases - Vector database for semantic search|Vector database for semantic search]] 
### Event-driven processing with Kafka
[[Data governance app with a RAG system - Event-driven processing with Kafka]]
## RAG system
[[Data governance app with a RAG system - RAG system]]
- [[Data governance app with a RAG system - Ray Serve]]
## Ray Serve
[[Data governance app with a RAG system - Ray Serve]]
# HTTP request queueing
We use Ray Serve to run a HTTP server and it provides request queueing.

The `max_ongoing_requests` parameter controls how many ongoing requests each replica can have, i.e. how many requests it can handle concurrently:
- A replica can have multiple requests in progress.
- It handles one request at a time.
- When it can't progress with one request because it waits for something (e.g. for reading data from a database), it can progress with other requests.

When we receive more requests  than the `max_ongoing_requests` parameter allows, the rest of them goes to the queue and waits for other requests to process.