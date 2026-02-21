Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
This is a guide for how to deploy code from this repo - [link](https://github.com/bulka4/data_and_ml_platform_kind) on a kind cluster for development.
# Starting the cluster
- Run the command from repo root folder:
```bash
# Run this from the repo root folder
kind create cluster --name data-platform --config kind-config.yaml
```
- Build and run the image for interacting with kind:
```bash
# Run this from the repo root folder
docker build -t interacting-kind -f interacting.kind.Dockerfile .
docker run -it --rm -v C:\Users\mbulka\.kube:/root/.kube interacting-kind bash
```
- Run the `/bin/bash /root/modify_kubeconfig.sh` script
# Cleanup
How to clean up resources when we are done.

Cleanup of Docker images:
```bash
# remove all containers
docker rm $(docker ps -aq)
# remove all images
docker rmi $(docker image ls -aq)
# remove everything (images, containers, cache, volumes)
docker system prune --all --volumes
```

Delete the kind cluster:
```bash
kind delete cluster --name data-platform
```
# Prepare images and Kubernetes secrets
- Run the `/root/dockerfiles/build_and_load.sh` script from the image on the host (run it outside of the image for interacting with kind. It requires Docker)
- Run the `/bin/sh /root/create_k8s_secrets.sh` command
# Airflow deployment
- Install Helm chart:
```bash
# Execute below commands from the helm_charts/airflow folder
helm dependency update

helm -n airflow install airflow . &
```
# Spark common resources deployment
Install Helm chart which creates resources in the `spark` namespace used by other Helm charts related to Spark (Spark Thrift Server and Hive metastore):
```bash
# Execute below commands from the helm_charts/spark_common folder
helm dependency update

helm -n spark install common . &
```
# Hive deployment
```bash
# Execute below commands from the helm_charts/hive_metastore folder
helm dependency update

helm -n spark install hive . &
```
# Spark Thrift Server deployment
- Install Helm chart:
```bash
# Execute below commands from the helm_charts/spark_thrift_server folder
helm -n spark install spark . &
```
