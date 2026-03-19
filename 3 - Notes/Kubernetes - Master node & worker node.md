Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
A master node is used to orchestrate containers with applications running on worker nodes.

Worker nodes are used to run containers.

When user wants to run a container, they communicate with a master node, and master node then communicates with worker nodes to run that container.

We have different processes running on a master node and worker nodes. They are explained in more detail in subsections below.
## Processes running on master and worker nodes
On a master node we have different processes running than on worker nodes.

The main processes we are running on a master node are:
- API Server - [[Kubernetes - Components - API server|link]] 
- Scheduler - [[Kubernetes - Components - Scheduler|link]] 
- Controller manager - [[Kubernetes - Components - Controller manager|link]] 
- ETCD - [[Kubernetes - Components - Etcd|link]] 

While on a worker node the main processes are:
- Container runtime - [[Kubernetes - Components - Container runtime|link]] 
- Kubelet - [[Kubernetes - Components - Kubelet|link]] 
- Kube proxy - [[Kubernetes - Components - Kube proxy|link]] 
