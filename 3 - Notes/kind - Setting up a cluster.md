Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
How to set up a kind cluster and use it for deploying Kubernetes resources refer to the documents below.

They show how to use kind for deploying example resources for data processing and ML:
- [[Data and ML platform - Setting up a kind cluster]]
- [[Data and ML platform - Dev repository guide (kind)]]
# Prerequisites
- We need to have Docker installed and running - [[Docker - Windows setup]]
## kind config file
- Create the `kind-config.yaml` file:
```yaml
# kind-config.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    extraPortMappings:
      # port on which cluster is listening. Using this port we communicate with the cluster using kubectl
      # so it needs to be used in the kubeconfig file
      - containerPort: 6443
        hostPort: 6443
        protocol: TCP
      # port for accessing services
      - containerPort: 30080
        hostPort: 8080
        protocol: TCP
    # Mount a host folder into the node container so it can be mounted into pods
    extraMounts:
      - hostPath: "C:/<repo-path>/volume_data"
        containerPath: /kind-pv-data
  - role: worker
    # Mount a host folder into the node container so it can be mounted into pods
    extraMounts:
      - hostPath: "C:/<repo-path>/volume_data"
        containerPath: /kind-pv-data
networking:
  disableDefaultCNI: false
```
# Starting the cluster
- Run the command from the folder where we have `kind-config.yaml` file:
```bash
kind create cluster --name data-platform --config kind-config.yaml
```
# Kubeconfig file
A kubeconfig file, needed to interact with the cluster, is saved in the `%USERPROFILE%\.kube\config` file (`%USERPROFILE%` is user's folder, for example `C:\Users\<user-name>`) automatically by kind when we create a cluster.