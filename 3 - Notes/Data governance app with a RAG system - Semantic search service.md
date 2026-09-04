Tags: [[__My_projects]]
#MyProjects 

# Introduction
Semantic search service is a separate service used by the data governance backend and RAG system.
# Running and using the REST API server
We can deploy the Ray Serve REST API server for semantic search in two modes:
- Production deployment
- Development deployment

Below subsections describe how to deploy the server in both modes and how to test it.
## Dependencies
To run the REST API server, no matter whether  we use the production or the development deployment mode, we need to prepare dependencies:
- Deploy the Milvus vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]])
	- Optionally also populate it with embeddings (more info here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline|link]])
## Production deployment
To run the Ray Serve app with the REST API server for semantic search in production, run the server by installing the Helm chart:
- Set up the `DOWNLOAD_MODEL` parameter in `values.yaml` to indicate whether we want to download a new model from Hugging Face or to use already saved model
- Install the Helm chart:
	```shell
	# Execute below commands from the helm_charts/semantic_search_rest_api folder
	helm dependency build
	helm -n semantic-search install ray-serve . &
	```
### Testing API
Check the status of the deployed `RayService` resource:
```shell
kubectl -n semantic-search get rayservice semantic-search-rayservice -o yaml
```

When we use the production deployment mode, for testing we can use the `k8s/network.yaml` pod:
```shell
# Deploy the pod
kubectl apply -f /root/k8s/network.yaml

# Connect to the pod's shell session
kubectl -n semantic-search exec -it network -- /bin/bash

# Make a REST API call to the Ray Serve HTTP server
curl -v --get http://semantic-search-rayservice-head:8000/search \
	--data-urlencode "query=customer orders"
```
where:
- `semantic-search-rayservice-head` is name of the service used by the Ray Serve resource
	- `semantic-search-rayservice` is name of the created `RayService` resource (defined in `values.yaml`)
## Development deployment
Using the development mode, we can:
- Start the Ray Serve app faster
- See its logs in the terminal where we start the app (in the development mode those logs are hidden in some files)

This is better for debugging the app's code.

To run the Ray Serve app with the REST API server for semantic search in the development mode for testing, we can deploy the `k8s/semantic_search.yaml` pod, connect to its shell session and use the `serve run` command:
- Set up the `DOWNLOAD_MODEL` parameter in `values.yaml` to indicate whether we want to download a new model from Hugging Face or to use already saved model
- Run below commands:
	```shell
	# Deploy the pod
	cd /root/k8s/semantic_search
	helm -n semantic-search install semantic-search . &
	
	# Connect to the pod's shell session
	kubectl -n semantic-search exec -it semantic-search -- /bin/bash
	
	# Go to the folder with the Ray Serve app (routes.py)
	cd routes
	
	# Run the Ray Serve app. Here:
	#   - `routes` is the name of the file with the Ray Serve app (without the ".py"
	#      extension)
	#   - `semantic_search_service` is the name of the Ray Serve bound deployment - 
	#      output of the APIClassName.bind() command, where APIClassName is name of the
	#      class where we define Rest API endpoints.
	serve run routes:semantic_search_service
	```
### Testing API
When we use the development deployment mode, for testing we can connect to the pod running Ray Serve:
```shell
# Connect to the pod running Ray Serve
kubectl -n semantic-search exec -it semantic-search -- /bin/bash

# Install curl
apt-get update && apt-get install -y curl

# Make a REST API call
curl -v --get http://localhost:8000/search \
	--data-urlencode "query=customer orders"
```

We do it this way because when running Ray Serve app using the `serve run` command, then it listens on `127.0.0.1`, so it accepts connections only from the same pod.
# Serving
Semantic search service will be served as:
- REST API endpoint
- MCP tool - which calls that REST API endpoint
## MCP tool
MCP will be used by AI agents ([[AI agents - MCP tools for agents|link]]) in the RAG systems because it standardizes the way how to:
- discover what tools are available
- provide descriptions what different tools do and what is an input for them
- how tools are invoked
- how tool results are structured

which will make it easier for AI agents to use this semantic search tool.

For the data governance backend, a REST API endpoint should be easier to use.

It is deployed using the `helm_charts/mcp_server` Helm chart. It uses the REST API endpoint deployed using the `helm_charts/semantic_search_rest_api` Helm chart.
## REST API server
- The REST API server is deployed using Ray Serve and routes are defined using FastAPI.
- We run Ray Serve using the `RayService` CR on Kubernetes.
- The Ray Serve app that we run needs to be saved as a `.zip` file (this is required by the `RayService` CR)
- It is deployed using the `helm_charts/semantic_search_rest_api` Helm chart.
- It provides routes:
	```python
	@app.get("/search")
	async def ask(self, query: str, top_k: int = 3) -> list[dict]:
	"""
	Function for semantic search. It returns a list of dictionaries in the 
	following format:
	[
		{
			#ID of the table document (taken from the database documentation 
			# database)
			'object_id': object_id_1,
			# One text chunk from the document
			'text_chunk': text_chunk_1
			# Similarity score for this text chunk and the given query
			'similarity_score': similarity_score_1
		},
		...
	]
	"""
	# embedding for the user's query
	sentence_embedding = self.model.run(query)
	
	results = self.milvus.search(
		collection_name=self.milvus_collection,
		data=sentence_embedding.tolist(),
		anns_field=self.embedding_field_name,
		limit=top_k,
		output_fields=[self.metadata_field_name, self.text_field_name],
		search_params={"params": {"nprobe": self.nprobe}},
	)
	
	return [
		{
			'object_id': result.entity
						   .get(self.metadata_field_name)
							.get(self.object_id_field_name),
			'text_chunk': result.entity.get(self.text_field_name),
			'similarity_score': result.get('distance'),
		}
		for result in results[0]
	]
	```
# Clients
Clients that use this service:
- RAG system 
- Data governance backend (used in the searching option which displays relevant documents to users)
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