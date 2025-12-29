Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Namespaces are a way for organizing resources in Kubernetes. They are groups containing specified resources.

Each namespace doesn’t have separate resources (nodes, CPU, RAM). They share common, cluster’s resources. They just provide a way to logically group resources.
## The kube-system Namespace
This namespace contains all the system pods which are running required Kubernetes services like kube proxy, kube scheduler, api server etc.

#Cloud #DevOps #DistributedComputing #DataEngineering 