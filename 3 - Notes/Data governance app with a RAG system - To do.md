Tags: [[__My_projects]]
#MyProjects 

# Next steps
## Documentation
Document the project and ideas for further improvements - [[Data governance app with a RAG system - To do - Documentation]]
## Others
- Check how Redis is used in the data gov backend for caching
- Add monitoring: logs, traces, metrics
- Maybe also add: 
	- additional logs printing in pods which will confirm that everything works fine with documentation describing how to check those logs
	- pods from which we can check how the data looks like with a documentation describing how to do this
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