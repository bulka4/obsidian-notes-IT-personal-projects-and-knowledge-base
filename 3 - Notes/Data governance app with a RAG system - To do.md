Tags: [[__My_projects]]
#MyProjects 

# Next steps
## Deploy the semantic search service
- Deploy the semantic search service as a separate service so it can be used by the RAG system and the data governance backend
- Deploy it as REST API endpoint and use that endpoint in the MCP tool

Status:
- FastAPI routes for the REST API are ready (but not tested yet)

To do:
- Test FastAPI routes (once we have some data in the vector db)
- Prepare a MCP tool that uses this REST API
## Deploy data governance backend
- Use the semantic search service (REST API) in the data governance backend
## Prepare embedding ingestion pipeline
Prepare embedding ingestion pipeline so we have some data in the vector db to test semantic search.
## RAG system
Deploy RAG system so it uses the same semantic search MCP tool.
## Others
- Check how Redis is used in the data gov backend for caching
# Improvements
## Data governance backend
- Deploy it on Kubernetes
- Allow for creating plugins for collecting metadata from different types of SQL databases (MySQL, Postgres etc.). Convert the current solution into one plugin
- Create UI for submitting questions to the RAG system
- Use a graph database for data lineage data. This would help to answer questions like:
	- Which jobs eventually affect this table?
	- Show every upstream dependency.
	- Find every object affected if this column changes.
## Semantic search engine
- Convert it into a separate service (currently it is a part of the data governance app)
- Set up a pipeline populating a vector db using table documentations
## Machine learning models
- Store LLMs used for semantic search in MLflow (potentially, or maybe ONNX will be enough)
## Metadata extraction
- Rewrite the code in Python - this code will be simpler than in JavaScript
- 