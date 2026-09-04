Tags: [[__My_projects]]
#MyProjects 

# To do
[[Data governance app with a RAG system - To do]]
# System features
- Creating tables and columns documentation
- Find relevant documents using a semantic search engine
- LLM answering questions based on a created documentation
- Data lineage graphs generated automatically for a specific MS SQL server (based on automatically extracted SQL scripts from views, procedures and jobs)
# System architecture
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
- [[Data governance app with a RAG system - Semantic search service]]
	- [[Data governance app with a RAG system - Embedding Ingestion Pipeline|Embedding Ingestion Pipeline]] 
	- [[Data governance app with a RAG system - Databases - Vector database for semantic search|Vector database for semantic search]] 
## Embedding Ingestion Pipeline
- Ingesting vector embeddings into the vector database using SQL database documentation created by users

More information:
- [[Data governance app with a RAG system - Embedding Ingestion Pipeline]]
	- [[Data governance app with a RAG system - Databases - Vector database for semantic search|Vector database for semantic search]] 
## RAG system
- Answering user questions using embeddings from the documentation

More information:
- [[Data governance app with a RAG system - RAG system]]

System architecture diagram (arrows indicates that one service uses / communicates with another):
![a](system_architecture_diagram.svg)
# Tools used
[[Data governance app with a RAG system - Tools used]]
- [[Data governance app with a RAG system - Tools used - Node.js|Node.js]] 
# Pods for testing tools and interacting with resources
We can prepare pods for testing tools and interacting with resources using YAML manifests from the `k8s` folder. 

Here's how we can use different pods:
- `milvus.yaml`, `mongo.yaml`, `ms_sql.yaml` - Interact with deployed databases (query their data)
- `nodejs.yaml` - Use Node.js (e.g. run scripts from the `services/metadata_extraction` folder)
- `semantic_search.yaml` - Test code from the `services/semantic_search` folder
- `network.yaml` - Tools for testing network (e.g. testing whether we can reach some services through a network, DNS resolution, make REST API calls, etc.)

We connect to the created pod using the `kubectl -n <namespace> exec -it <pod-name> -- /bin/bash` command and inside of the pod we can use tools like it is described in this pod's YAML manifest.
# Infrastructure setup guide
[[Data governance app with a RAG system - Infrastructure setup guide]].
# Infrastructure
- [[Data governance app with a RAG system - Kind (kubernetes cluster in Docker)]]
- [[Data governance app with a RAG system - Docker image for interacting with kind]]
- [[Data governance app with a RAG system - VS Code Kubernetes extension setup for code development]]
- [[Data governance app with a RAG system - Docker images]]