Tags: [[__My_projects]]
#MyProjects 

# Introduction
This document describes Ray Serve which we use for running a REST API server with endpoints for semantic search and generating answers using the RAG system.
# Deployment details
- Ray Serve app that we deploy needs to be saved as a `.zip` file. It needs to be a folder containing all the files for the app. Currently we deploy the `services/semantic_search/routes.zip` file which is zipped `routes` folder.
- 
# Debugging
## Ray pod logs
Check logs of pods running Ray head and worker - `rag-rayservice-xxx-head-xxx` and `rag-rayservice-xxx-small-group-worker-xxx`.
## `RayService` resource status
Check the status of the deployed `RayService` resource:
```shell
kubectl -n semantic-search get rayservice rag-rayservice -o yaml
```
