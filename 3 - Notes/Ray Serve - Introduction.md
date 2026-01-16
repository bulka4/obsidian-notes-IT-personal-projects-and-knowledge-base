Tags: [[__Machine_Learning_Engineering]]

# Introduction
Ray Serve is a framework for serving long running Python services that can be accessed via HTTP, gRPC, or directly through Ray APIs. 

Usually it is used to serve ML models as Rest APIs. For example we can define REST API endpoints using FastAPI and Ray Serve will:
- Create multiple replicas
	- Each replica is a process that executes code for requests and prepares a response
	- They are ran on multiple nodes (servers) in a cluster (each process can be ran on a different server. That cluster can be prepared using Ray Core)
	- They can handle requests independently
- Run a proxy which will be receiving HTTP requests and forwarding them to replicas

We can also expose plain Python functions/classes accessible through Ray APIs.

#MLEngineering 