Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
In Kubernetes we create a cluster consisting of many nodes (servers). Kubernetes helps us with scheduling our applications, i.e. we specify what application we want to run, Kubernetes finds a proper node and run our app on it.

Kubernetes is for running containerized applications, for example Docker containers.

We specify what application to run and how using a YAML file. For example, we can specify there:
- What Docker image to use
- What shell command to execute
- How to set up environment variables
- How to mount external storage to a Docker container

Kubernetes helps with allocating computer resources (CPU, RAM etc.) to applications. In that aspect, it is like a kernel but for a cluster consisting of multiple servers.

It also helps with networking between containers. Each container can get assigned easily a static IP address and a DNS name.
