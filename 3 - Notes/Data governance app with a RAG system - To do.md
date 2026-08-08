Tags: [[__My_projects]]
#MyProjects 

# Next steps
- Deploy a MS SQL server from which we will collect metadata
	- When deploying it, run a SQL script that creates a few tables, views and procedures
- Deploy data governance backend and semantic search service on Kubernetes
	- Deploy the semantic search service as a separate service so it can be used by the RAG system as well
	- Use Ray Serve optionally for it as it will be used for the RAG system
- Deploy RAG system so it uses the same semantic search engine as the data governance backend
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