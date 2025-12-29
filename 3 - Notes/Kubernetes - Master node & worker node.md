Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
A master node is used to orchestrate containers with applications running on worker nodes.

Worker nodes are used to run containers.

When user wants to run a container, they communicate with a master node, and master node then communicates with worker nodes to run that container.

We have different processes running on a master node and worker nodes. They are explained in more detail in subsections below.
## Processes running on master and worker nodes
On a master node we have different processes running than on worker nodes.

The main processes we are running on a master node are:
- API Server
- Scheduler
- Controller manager
- ETCD

While on a worker node the main processes are:
- Container runtime
- Kubelet
- Kube proxy
### Container runtime
Each node needs to have installed a container runtime, like docker or containerd, which will be running containers.
### Kubelet
It is a process running containers on nodes. It interacts with a container and node. It creates containers based on provided configuration, YAML manifests.
### Kube proxy
It forwards requests from Services to Pods.  
### API server
Users interacting with Kubernetes cluster are using the API server. It takes requests from users about what they want to do with a cluster, and then API server talks to other processes running on Kubernetes.

It is also used for authentication.
### Scheduler
API server talks to the Scheduler and Scheduler decides on which node to run requested Pods. It check how much resources (CPU, RAM) will be needed for running a Pod, and which nodes have those resources available.

Scheduler doesn’t run the app itself but it talks to the kubelet and kubelet runs an app.
### Controller manager
It monitors the state of Pods, if they are running correctly or if they have died. If a Pod died then Controller manager talks to the Scheduler in order to rerun a Pod.
### Etcd
Etcd Stores data about all the changes that happens in a Kubernetes cluster, for example when Pod dies, and when a new Pod gets created.

It provides data used by other servicer (API server, Scheduler, Controller manager).

#Cloud #DevOps #DistributedComputing #DataEngineering 