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
## Prepare images
Run commands from the `/bash/build_and_load_images.sh` script on the host (run them outside of the container for interacting with kind. They require to use Docker)

It builds Docker images and loads them to kind, so they can be used to run pods
# Connect to kind
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
# Prepare Kubernetes resources
From inside of the image for interacting with Kubernetes run the command:
> `bash /root/bash/create_k8s_secrets.sh`

This creates Kubernetes resources like namespaces and secrets we will be using.
# Running the system
## Extract SQL server metadata
Prepare source SQL server metadata in the MongoDB for which we will be creating documentation in the Data Governance app:
- Install the source MS SQL Server:
	- From which we will extract metadata
  ```bash
	helm -n source-db install ms-sql /root/helm_charts/ms_sql &
  ```
- Install the MongoDB Helm chart:
	- Where we will save extracted metadata
  ```bash
	helm dependency build /root/helm_charts/mongo_db
	helm -n semantic-search install mongo-db /root/helm_charts/mongo_db &
  ```
- install the Metadata Extraction Helm chart:
	- Which runs a script for extracting metadata from the source SQL server into the MongoDB
  ```bash
	helm -n semantic-search install metadata-extraction /root/helm_charts/metadata_extraction &
  ```
## Embedding ingestion service
To run the embedding ingestion service ([[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service|link]]):
- Install the Milvus Helm chart:
	- It will deploy Milvus and create a collection in Milvus that will be used to store embeddings
	- In Milvus we will store vector embeddings
    ```bash
	helm dependency build /root/helm_charts/create_milvus_collection
	helm -n semantic-search install milvus /root/helm_charts/create_milvus_collection . &
    ```
- Install Kafka Helm chart:
	```shell
	helm dependency build /root/helm_charts/kafka
	helm -n semantic-search install kafka /root/helm_charts/kafka . &
	```
- Create a topic in Kafka, where data governance backend will be emitting messages and embedding ingestion service will read messages from:
  ```shell
  kubectl -n semantic-search exec -it kafka-controller-0 \
	  -- kafka-topics.sh \
		  --create --topic table-descriptions \
		  --bootstrap-server kafka:9092 \
		  --partitions 1 \
		  --replication-factor 1
  ```
- Install the embedding ingestion service Helm chart:
  ```bash
	helm -n semantic-search install emb-ing /root/helm_charts/embedding_ingestion_service &
  ```
## Data Governance Backend
Deploy the Data Governance Backend:
- Install the Redis Helm chart:
	- Redis is used for caching in this backend
  ```bash
	helm dependency build /root/helm_charts/redis
	helm -n semantic-search install redis /root/helm_charts/redis &
  ```
- install the Data Governance Backend Helm chart:
  ```bash
	helm -n semantic-search install data-gov /root/helm_charts/data_gov_backend/ &
  ```
- It takes a few minutes to start the app. In the pod's logs we should see after some time logs `Connection to Redis is ready` and `app started listening to requests`
- Access data governance UI using this URL in a browser: `localhost:8080`
- Log in using username `admin@admin.com` and password `admin`
- Using UI, create descriptions for tables which will be used for the semantic search and RAG system
## MCP server
Run the MCP server providing a tool for semantic search. It uses the semantic search endpoint from created REST API server and it is used by the RAG endpoint from the save server:
- Install the MCP server Helm chart:
	```shell
	helm -n semantic-search install mcp /root/helm_charts/mcp_server &
	```
## RAG REST API server
To run the RAG REST API server which provides endpoints for answering questions using a RAG system and semantic search:
- Install the RAG Helm chart (It will run a REST API server using Ray Serve):
  ```shell
	helm dependency build /root/helm_charts/rag_rest_api
	helm -n semantic-search install rag /root/helm_charts/rag_rest_api &
  ```