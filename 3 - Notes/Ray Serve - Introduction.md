Tags: [[__Machine_Learning_Engineering]] [[_Ray]]
#MLEngineering #Ray 

# Introduction
Ray Serve is a distributed model serving framework built on top of Ray ([[_Ray|link]]). It’s used to serve Python functions (enable other applications to use them), especially ones using ML models.

It creates:
- Multiple replicas of workers which will execute code (Python functions requested by clients (other applications)). They can:
	- Run on different servers
	- Execute different tasks in parallel
- A proxy that:
	- Receives requests from clients 
	- Forwards it to workers to execute functions
	- Sends back the function's result to the client.
  
  That proxy can be a HTTP server but it can also use other protocols for communication with clients, e.g. Ray's own RPS mechanism.

When serving using a HTTP server, in order to define endpoints we can use either Ray Serve itself or another framework, for example FastAPI.
# How it works
## 1. Define deployment
We define a deployment which is a Python function.
## 2. Ray turns them into distributed actors
Ray runs each deployment as:
- Multiple replicas (each one can handle requests from other applications independently)
- Distributed workers across nodes (each one can handle different tasks from the request)
## 3. Request routing layer
Ray Serve includes a built-in HTTP server that:
- receives requests
- routes them to the correct deployment
- balances load across replicas
- handles retries/failures
## 4. Autoscaling and scheduling
Because it runs on Ray:
- it can scale replicas up/down based on traffic
- distribute work across a cluster
- place models on GPUs or CPUs intelligently
# Benefits
Ray Serve takes care of:
- Load balancing
- autoscaling
- request routing
- batching
- replication
- distributed task execution (different tasks from a request can be handled in parallel)
