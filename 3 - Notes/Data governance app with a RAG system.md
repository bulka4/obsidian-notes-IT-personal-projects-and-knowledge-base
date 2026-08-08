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
- Data governance backend ([[Data governance app with a RAG system - Data governance backend|link]])
	- Serving UI
	- Handling authentication and authorization
- Semantic search service ([[Data governance app with a RAG system - Semantic search service|link]])
	- Providing semantic search functionality
- Metadata extraction ([[Data governance app with a RAG system - Metadata extraction|link]])
	- Extracting and saving metadata from a SQL database (info about tables, columns, sql scripts from views, jobs etc.)
- Embedding Ingestion Pipeline ([[Data governance app with a RAG system - Embedding Ingestion Pipeline|link]])
	- Ingesting vector embeddings into the vector database using SQL database documentation created by users
- RAG system ([[Data governance app with a RAG system - RAG system|link]])
	- Answering user questions using embeddings from the documentation

System architecture diagram (arrows indicates that one service uses / communicates with another):
![a](system_architecture_diagram.svg)
# Tools used
[[Data governance app with a RAG system - Tools used]]
# Source MS SQL Server
As a part of this project, we deploy on Kubernetes our own MS SQL Server from which we collect metadata and for which we create documentation in the data governance app.

More information is here - [[Data governance app with a RAG system - Source MS SQL Server]].
# Infrastructure setup guide
[[Data governance app with a RAG system - Infrastructure setup guide]].
# Infrastructure
- [[Data governance app with a RAG system - Kind (kubernetes cluster in Docker)]]
- [[Data governance app with a RAG system - Docker image for interacting with kind]]
- [[Data governance app with a RAG system - VS Code Kubernetes extension setup for code development]]