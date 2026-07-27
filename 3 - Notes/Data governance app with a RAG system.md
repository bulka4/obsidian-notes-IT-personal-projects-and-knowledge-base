Tags: [[__My_projects]]
#MyProjects 

# High-level plan
- Deploy data governance app on Kubernetes
- Set up a pipeline populating a vector db using table documentations
- Create UI for submitting questions to the RAG system
# System features
- Creating tables and columns documentation
- Find relevant documents using a semantic search engine
- LLM answering questions based on a created documentation
- Data lineage graphs generated automatically for a specific MS SQL server (based on automatically extracted SQL scripts from views, procedures and jobs)
# System architecture
- Everything deployed on Kubernetes
- Data pipeline running on schedule populating a vector database for semantic search

 Documents for specific parts of the systems:
- Data governance app - [[Data governance app with a RAG system - Data governance app|link]] 
- Semantic search engine - [[Data governance app with a RAG system - Semantic search engine|link]] 
- RAG system - [[Data governance app with a RAG system - RAG system|link]] 
# To do
[[Data governance app with a RAG system - To do]]