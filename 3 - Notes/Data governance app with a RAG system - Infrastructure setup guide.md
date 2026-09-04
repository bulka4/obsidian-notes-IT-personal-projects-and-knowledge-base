Tags: [[__My_projects]]
#MyProjects 

# Introduction
This is a guide for how to set up all the infrastructure needed to run the code from this repo - (link) on a kind cluster for development.

We assume here that we already have:
- Azure account
- Terraform, Docker and kind installed
# Kind cluster setup
Set up a kind cluster and Docker image for interacting with it ([[Data governance app with a RAG system - Kind (kubernetes cluster in Docker)|link]], [[Data governance app with a RAG system - Docker image for interacting with kind|link]]):
- Start Docker engine
- Start the kind cluster:
```bash
# Run this from the repo root folder
kind create cluster --name data-gov --config kind-config.yaml
```
- Copy the `.kube` folder (usually located at `C:\Users\username`) into the repo root folder (so it can be copied into the image we build in the next step)
- Build and run the image for interacting with kind:
```bash
# Run this from the repo root folder
docker build -t interacting-kind -f interacting.kind.Dockerfile .
docker run -it --rm interacting-kind bash
```
# (Optional) VS Code for code development on Kubernetes
If we want to use VS Code to connect to Kubernetes pods and be able to modify files there and run commands in a terminal, we need to additionally modify the kubeconfig file to allow VS Code to connect to the Kubernetes cluster:
- Kubeconfig file is usually located at `C:\Users\username\.kube\config`)
- We need to modify it and change the IP address from `0.0.0.0` to `127.0.0.1` in the `clusters.cluster_name.server` field, for the kind cluster.
# Cleanup
How to clean up resources when we are done.

Cleanup of Docker images:
```bash
# stop all the containers
docker stop $(docker ps -aq)

# remove all containers
docker rm $(docker ps -aq)

# remove all images
docker rmi $(docker image ls -aq)

# remove build cache
docker image prune -a
docker builder prune -a

# remove everything (images, containers, cache, volumes)
docker system prune --all --volumes
```

Delete the kind cluster:
```bash
kind delete cluster --name data-platform
```

Sometimes, on Windows, using `docker prune` might not release disk space or it doesn't work because we don't have any disk space left. Then, what we can do is:
- close docker desktop
- shutdown wsl - run in terminal: `wsl --shutdown`
- Delete the file (Docker virtual disk): `C:\Users\<username>\AppData\Local\Docker\wsl\disk\ext4.vhdx`
# Prepare images and Kubernetes secrets
From inside of the image for interacting with Kubernetes:
- Run the `bash /root/bash/create_k8s_secrets.sh` command
	- To create Kubernetes namespaces and secrets we will be using
- Run commands from the `/bash/build_and_load_images.sh` script on the host (run them outside of the container for interacting with kind. They require to use Docker)
	- It builds Docker images and loads them to kind, so they can be used to run pods
# Running the system
## Extract SQL server metadata
Prepare source SQL server metadata in the MongoDB for which we will be creating documentation in the Data Governance app:
- Install the source MS SQL Server:
	- From which we will extract metadata
  ```bash
	# Execute below commands from the helm_charts/ms_sql folder
	helm -n source-db install ms-sql . &
  ```
- Install the MongoDB Helm chart:
	- Where we will save extracted metdata
  ```bash
  	# Execute below commands from the helm_charts/mongo_db folder
	helm dependency build
	helm -n semantic-search install mongo-db . &
  ```
- install the Metadata Extraction Helm chart:
	- Which runs a script for extracting metadata from the source SQL server into the MongoDB
  ```bash
	# Execute below commands from the helm_charts/metadata_extraction folder
	helm -n semantic-search install metadata-extraction . &
  ```
## Data Governance Backend
Deploy the Data Governance Backend:
- Install the Redis Helm chart:
	- Redis is used for caching in this backend
  ```bash
	# Execute below commands from the helm_charts/redis folder
	helm dependency build
	helm -n semantic-search install redis . &
  ```
- install the Data Governance Backend Helm chart:
  ```bash
	# Execute below commands from the helm_charts/data_gov_backend folder
	helm -n semantic-search install data-gov . &
  ```
- Access data governance app using this URL in a browser: `localhost:8080`
## Embedding ingestion pipeline
The embedding ingestion pipeline will ingest embeddings into the vector database using tables descriptions created by us using the Data Governance UI.

To create descriptions:
- access UI at the URL `localhost:8080`
- go to the `Data catalog` section
- select a table from the left-hand side panel
- create a description and click on `save`

To run the embedding ingestion pipeline:
- Install the Milvus Helm chart:
	- It will deploy Milvus and create a collection in Milvus that will be used to store embeddings
	- In Milvus we will store vector embeddings
    ```bash
	# Execute below commands from the helm_charts/create_milvus_collection folder
	helm dependency build
	helm -n semantic-search install milvus . &
    ```
- Install the Embedding ingestion pipeline Helm chart:
  ```bash
	# Execute below commands from the helm_charts/embedding_ingestion_pipeline folder
	helm -n semantic-search install emb-ing . &
  ```
## Semantic search REST API server
To run the Semantic search REST API server:
- Install the Semantic search Helm chart:
	- It will run a REST API server using Ray Serve
  ```shell
	# Execute below commands from the helm_charts/semantic_search_rest_api folder
	helm dependency build
	helm -n semantic-search install ray-serve . &
  ```
## MCP server
Run the MCP server providing a tool for semantic search (that uses the created REST API server):
- Install the MCP server Helm chart:
	```shell
	# Execute below commands from the helm_charts/mcp_server folder
	helm -n semantic-search install mcp . &
	```