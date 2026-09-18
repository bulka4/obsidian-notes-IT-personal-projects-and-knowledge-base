Tags: [[__My_projects]]
#MyProjects 

# Introduction
The `k8s` folder contains YAML manifests of pods that we can use for debugging. We can connect to a shell session of those pods and interact with other services.

For example, we can use the `network.yaml` pod to test REST APIs:
```shell
# Deploy the pod
kubectl apply -f /root/k8s/network.yaml

# Connect to the pod's shell session
kubectl -n semantic-search exec -it network -- /bin/bash

# Make a REST API call to the Ray Serve HTTP server
curl -X POST http://rag-rayservice-head:8000/ask \
  -H "Content-Type: application/json" \
  -d '{"query":"which table contains data about orders","top_k":3}'
```
# Pods
Below is a list of pods that we can use and how to use them:
- `semantic_search`
	- testing code from the `semantic_search` folder and the `semantic-search` Docker image
	- Prepare and use model from Hugging Face for generating embeddings
	- Run the `services/semantic_search/model_preparation/download_model.sh` script for downloading a model from HuggingFace
	- Run the `services/semantic_search/model_preparation/load_model.py` script for loading a model and generating an output with it
	- Run code used in the Ray Serve app for semantic search (the `routes/routes.py` script)
- 