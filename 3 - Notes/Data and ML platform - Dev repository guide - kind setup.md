Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
This is a guide for how to deploy code from this repo - [link](https://github.com/bulka4/data_and_ml_platform_kind) on a kind cluster for development. 

That is code from the Data and ML platform project about which more info we can find here - [[Data and ML platform project]].
# Starting the cluster
- Run the command from repo root folder:
```bash
# Run this from the repo root folder
kind create cluster --name data-platform --config kind-config.yaml
```
- Copy the `.kube` folder (usually located at `C:\Users\username`) into the repo root folder (so it can be copied into the image we build in the next step)
- Build and run the image for interacting with kind:
```bash
# Run this from the repo root folder
docker build -t interacting-kind -f interacting.kind.Dockerfile .
docker run -it --rm interacting-kind bash
```
# (Optional) set resources limits for kind nodes
Optionally we can set resource limits on kind nodes container so that the control plane doesn't take too much resources (and we won't run any pods on it) and assign more resources to the worker node (and run all the pods on it):
```bash
docker update --cpus="1.0" --memory="2g" --memory-swap="2g" data-platform-control-plane

docker update --cpus="5.0" --memory="10g" --memory-swap="10g" data-platform-worker
```
# (Optional) VS Code for code development on Kubernetes
If we want to use VS Code to connect to Kubernetes pods and be able to modify files there and run commands in a terminal, we need to additionally modify the kubeconfig file to allow VS Code to connect to the Kubernetes cluster:
- Kubeconfig file is usually located at `C:\Users\username\.kube\config`)
- We need to modify it and change the IP address from `0.0.0.0` to `127.0.0.1` in the `clusters.cluster_name.server` field, for the kind cluster.
# Cleanup
How to clean up resources when we are done.

Cleanup of Docker images:
```bash
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
# Prepare images and Kubernetes secrets
- Run the `/bin/sh /root/create_k8s_secrets.sh` command
- Run the `/root/dockerfiles/build_and_load.sh` script from the image on the host (run it outside of the image for interacting with kind. It requires Docker)
# Installing helm charts
- Install git-sync chart
	- It pulls code from a git repo and saves it in a PV
	- Airflow uses the code pulled by it
  ```bash
	# Execute below commands from the helm_charts/git_sync folder
	helm -n git-sync install git-sync . &
  ```
- Install Airflow:
	```bash
	# Execute below commands from the helm_charts/airflow folder
	helm dependency update
	helm -n airflow install airflow . &
	```
- Install Spark Thrift Server
	```bash
	# Execute below commands from the helm_charts/spark_thrift_server folder
	helm -n spark install spark . &
	```
- Install MLflow tracking server
	- And also service account used by the `mlflow_project` helm chart
  ```bash
	# Execute below commands from the helm_charts/mlflow_setup folder
	helm -n mlflow install mlflow . &
  ```
