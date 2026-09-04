Tags: [[__My_projects]]
#MyProjects 

# Next steps
## Use the new semantic search REST API in the Data Governance Backend
[[Data governance app with a RAG system - To do - Use the new semantic search REST API in the Data Governance Backend]]
## Automate embedding ingestion pipeline
Automate embedding ingestion pipeline such that it is triggered every time we save table description.
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