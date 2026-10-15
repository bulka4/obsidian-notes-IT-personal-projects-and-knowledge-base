Tags: [[__My_projects]]
#MyProjects 

# To do
[[Data governance app with a RAG system - To do]]
# System features
- Creating tables and columns documentation
- Find relevant documents using a semantic search engine
- RAG system answering questions based on a created documentation
- Data lineage graphs generated automatically for a specific MS SQL server (based on automatically extracted SQL scripts from views, procedures and jobs)
# System design
[[Data governance app with a RAG system - System design]]
# System architecture
[[Data governance app with a RAG system - System architecture]]
# Error handling
How the system handles errors - [[Data governance app with a RAG system - Error handling]]
# Infrastructure setup guide
[[Data governance app with a RAG system - Infrastructure setup guide]].
# Pods for testing tools and interacting with resources
We can prepare pods for testing tools and interacting with resources using YAML manifests from the `k8s` folder. 

Here's how we can use different pods:
- `milvus.yaml`, `mongo.yaml`, `ms_sql.yaml` - Interact with deployed databases (query their data)
- `nodejs.yaml` - Use Node.js (e.g. run scripts from the `services/metadata_extraction` folder)
- `semantic_search.yaml` - Test code from the `services/semantic_search` folder
- `network.yaml` - Tools for testing network (e.g. testing whether we can reach some services through a network, DNS resolution, make REST API calls, etc.)

We connect to the created pod using the `kubectl -n <namespace> exec -it <pod-name> -- /bin/bash` command and inside of the pod we can use tools like it is described in this pod's YAML manifest.
# Infrastructure
- [[Data governance app with a RAG system - Kind (kubernetes cluster in Docker)]]
- [[Data governance app with a RAG system - Docker image for interacting with kind]]
- [[Data governance app with a RAG system - VS Code Kubernetes extension setup for code development]]
- [[Data governance app with a RAG system - Docker images]]
# Tools used
[[Data governance app with a RAG system - Tools used]]
- [[Data governance app with a RAG system - Tools used - Node.js|Node.js]] 
# Debugging
Tips for debugging:
- [[Data governance app with a RAG system - Debugging pods]]
- [[Data governance app with a RAG system - Kafka debugging]]