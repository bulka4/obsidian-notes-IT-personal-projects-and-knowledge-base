Tags: [[__My_projects]]
#MyProjects 

# Introduction
Semantic search API is a REST API server providing an endpoint for semantic search.

It is used by the data governance backend and the RAG system (for the RAG system it is used via a MCP tool).

It is deployed together with the endpoint for generating answers using the RAG system, using the same `RayService` Kubernetes CR. It should be deployed separately though, using another `RayService` Kubernetes CR, but we might not have enough computational resources for that so both endpoints are deployed together.
# Running and using the REST API server
[[Data governance app with a RAG system - Semantic search API - Running and using the REST API server]]
# Architecture
[[Data governance app with a RAG system - Semantic search API - Architecture]]
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

It is deployed using the `helm_charts/mcp_server` Helm chart. It uses the REST API endpoint deployed using the `helm_charts/rag_rest_api` Helm chart.
## REST API server
- The REST API server is deployed using Ray Serve and routes are defined using FastAPI.
- We run Ray Serve using the `RayService` CR on Kubernetes.
- The Ray Serve app that we run needs to be saved as a `.zip` file (this is required by the `RayService` CR)
- It is deployed using the `helm_charts/rag_rest_api` Helm chart.
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
Pipeline ingesting embeddings into a vector database that will be used for a semantic search is described here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service]].
# Model for generating embeddings
If we don't have a model for generating embeddings yet, then we need to download one from Hugging Face.

We can do this by setting up env vars in the `values.yaml` file under the `env` field:
- `DOWNLOAD_EMBEDDING_MODEL: "True"` 
- `EMBEDDING_MODEL_NAME: sentence-transformers/all-MiniLM-L6-v2`

It will download a model and save it in the ONNX format, so the next time we want to run the Ray app, we can used this saved model by setting up env vars in the `values.yaml` file:
- `DOWNLOAD_EMBEDDING_MODEL: "False"`
- `EMBEDDING_MODEL_NAME: `
- `EMBEDDING_MODEL_PATH: /app/ml_models/embeddings/all-MiniLM-L6-v2`
## Model storage - other options
Instead of storing a model locally, we could also store it in the cloud (e.g. Azure Storage Account).

We could also use MLflow if we need to manage multiple models and versions, train our own models or attach some metadata to models but for this project this is not needed.
## Downloading and using the model
Bash script that downloads the model using the `optimum-cli` CLI tool:
> `services/semantic_search/model_preparation/download_model.sh`

In order to see how to load and use the saved model, use this python script:
> `services/semantic_search/model_preparation/load_model.py`

The same code is also used in the script:
> `services/semantic_search/routes/interface_implementations/TransformersEmbeddingModel.py` 
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
# Ray Serve details
More details about Ray Serve which we use for deploying the Semantic search API, including deployment and debugging, are here - [[Data governance app with a RAG system - Ray Serve]].