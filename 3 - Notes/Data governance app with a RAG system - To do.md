Tags: [[__My_projects]]
#MyProjects 

# Improvements
## Data governance app
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