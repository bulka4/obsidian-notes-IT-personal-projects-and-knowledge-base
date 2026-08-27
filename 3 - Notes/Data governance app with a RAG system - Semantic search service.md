Tags: [[__My_projects]]
#MyProjects 

# Introduction
Semantic search service is a separate service used by the data governance backend and RAG system.
# Running and using the REST API server
To run the REST API server, we need to prepare dependencies:
- Deploy the Milvus vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]])
	- Optionally also populate it with embeddings (more info here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline|link]])

Below subsections explain how to run further the Ray Serve app with the REST API server for semantic search in two modes:
- Production deployment
- Development testing
## Production deployment
To run the Ray Serve app with the REST API server for semantic search in production, run the server by installing the Helm chart:
```shell
# Execute below commands from the helm_charts/semantic_search_rest_api folder
helm dependency build
helm -n semantic-search install ray-serve . &
```
## Development testing
To run the Ray Serve app with the REST API server for semantic search in the development mode for testing, we can deploy the `k8s/semantic_search.yaml` pod, connect to its shell session and use the `serve run` command:
```shell
# Deploy the pod
kubectl apply -f /root/k8s/semantic_search.yaml

# Connect to the pod's shell session
kubectl -n semantic-search exec -it semantic-search -- /bin/bash

# Run the Ray Serve app. Here:
#   - `routes` is the name of the file with the Ray Serve app (without the ".py"
#      extension)
#   - `semantic_search_service` is the name of the Ray Serve bound deployment - 
#      output of the APIClassName.bind() command, where APIClassName is name of the
#      class where we define Rest API endpoints.
serve run routes:semantic_search_service
```
## Testing API
To test the API, we can use the `k8s/network.yaml` pod:
```shell
# Deploy the pod
kubectl apply -f /root/k8s/network.yaml

# Connect to the pod's shell session
kubectl -n semantic-search exec -it network -- /bin/bash

# Make a REST API call
curl -v --get http://semantic-search-rayservice-head:8000/search \
	--data-urlencode "query=customer orders"
```
where:
- `semantic-search-rayservice-head` is name of the service used by the Ray Serve resource
	- `semantic-search-rayservice` is name of the created `RayService` resource (defined in `values.yaml`)
# Serving
Semantic search service will be served as:
- REST API endpoint
- MCP tool - which calls that REST API endpoint

MCP will be used by AI agents in the RAG systems because it standardizes the way how to ([[AI agents - MCP tools for agents|link]]):
- discover what tools are available
- provide descriptions what different tools do and what is an input for them
- how tools are invoked
- how tool results are structured

which will make it easier for AI agents to use this semantic search tool.

For the data governance backend, a REST API endpoint should be easier to use.
## REST API server
- The REST API server is deployed using Ray Serve and routes are defined using FastAPI.
- We run Ray Serve using the `RayService` CR on Kubernetes.
- The Ray Serve app that we run needs to be saved as a `.zip` file (this is required by the `RayService` CR)
# Clients
Clients that use this service:
- RAG system 
- Data governance backend (used in the searching option which displays relevant documents to users)
# Data model
Data model used in a vector database for semantic search looks like that:
```
Collection: document_chunks

id | vector        | text_chunk              | metadata
---+---------------+-------------------------+-------------------------
1  | [0.1,0.2...]  | "SQL joins combine..."  | {
                                                document_id: 1,
                                                chunk_id: 1
                                              }
2  | [0.4,0.8...]  | "Indexes improve..."    | {
                                                document_id: 1,
                                                chunk_id: 2
                                              }
3  | [0.3,0.5...]  | "MongoDB stores..."    | {
                                                document_id: 2,
                                                chunk_id: 1
                                              }
```

where:
- we have one collection for all text documents for which we create embeddings
- each record in that collection corresponds to one text chunk
- metadata indicates which document that text chunk belongs to

Metadata to include:
- `database`
- `schema`
- `object_type` - table or column
- `object_name` - table or column name
- `object_id` 
- `chunk_id`

Include this metadata to enable filtering.
# Vector database for embeddings
Embeddings will be stored in the Milvus like described here - [[Data governance app with a RAG system - Databases - Vector database for semantic search]].
## Embedding ingestion pipeline
Pipeline ingesting embeddings into a vector database that will be used for a semantic search is described here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline]].
# Model preparation
Model used for semantic search is downloaded by a bash script from HuggingFace and stored on a local machine in the ONNX format. It could be also stored in cloud (e.g. Azure Storage Account).

We could also use MLflow if we need to manage multiple models and versions, train our own models or attach some metadata to models but for this project this is not needed.
## Downloading and using the model
Bash script that downloads the model:
> `services/semantic_search/model_preparation/download_model.sh`

In order to see how to load and use the saved model, use this python script:
> `services/semantic_search/model_preparation/load_model.py`

The `Dockerfile` and `requirements.txt` files from the `services/semantic_search/model_preparation` folder are used to prepare an environment to run the bash script for downloading the model and python script for loading and using this model.
## Testing downloading and using the model
In order to test downloading and using the model, we can create a testing pod:
```bash
# Create a testing pod
kubectl apply -f k8s/test_model_preparation.yaml

# Connect to the pod
kubectl -n semantic-search exec -it model -- /bin/bash

# Run the script for downloading a model
bash download_model.sh

# Run the script for loading a model and generating an output with it
python3 load_model.py
```