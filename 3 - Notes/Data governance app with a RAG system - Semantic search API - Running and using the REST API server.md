Tags: [[__My_projects]]
#MyProjects 

# Introduction
We can deploy the Ray Serve REST API server for semantic search in two modes:
- Production deployment
- Development deployment

Below subsections describe how to deploy the server in both modes and how to test it.
# Dependencies
To run the REST API server, no matter whether  we use the production or the development deployment mode, we need to prepare dependencies:
- Deploy the Milvus vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]])
	- Optionally also populate it with embeddings (more info here - [[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|link]])
# Production deployment
To run the Ray Serve app with the REST API server for semantic search in production, run the server by installing the Helm chart:
- Set up the `DOWNLOAD_MODEL` parameter in `values.yaml` to indicate whether we want to download a new model from Hugging Face or to use already saved model
- Install the Helm chart:
	```shell
	# Execute below commands from the helm_charts/rag_rest_api folder
	helm dependency build
	helm -n semantic-search install rag . &
	```

This will run the `rag-rayservice-xxx-head-xxx` and `rag-rayservice-xxx-small-group-worker-xxx` pods, running Ray head and worker. If we don't have enough resources for the worker, then the head pod will run the proxy handling requests.

We can check there logs for errors.
## Testing API
Check the status of the deployed `RayService` resource:
```shell
kubectl -n semantic-search get rayservice rag-rayservice -o yaml
```

When we use the production deployment mode, for testing we can use the `k8s/network.yaml` pod:
```shell
# Deploy the pod
kubectl apply -f /root/k8s/network.yaml

# Connect to the pod's shell session
kubectl -n semantic-search exec -it network -- /bin/bash

# Make a REST API call to the Ray Serve HTTP server
curl -v --get http://rag-rayservice-head:8000/search \
	--data-urlencode "query=customer orders"
```
where:
- `rag-rayservice-head` is name of the service used by the Ray Serve resource
	- `rag-rayservice` is name of the created `RayService` resource (defined in `values.yaml`)
# Development deployment
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
	#   - `rag_service` is the name of the Ray Serve bound deployment - 
	#      output of the APIClassName.bind() command, where APIClassName is name of the
	#      class where we define Rest API endpoints.
	serve run routes:rag_service
	```
## Testing API
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