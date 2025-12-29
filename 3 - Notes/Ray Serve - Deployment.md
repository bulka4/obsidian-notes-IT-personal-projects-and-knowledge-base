Tags: [[__Machine_Learning_Engineering]]

# Introduction
Deployment is an object used for running a long-running service, for example a Rest API.

We typically create a Deployment by creating a Python class decorated with @serve.deployment. Its methods can for example specify how to handle HTTP endpoints:
![[2 - Images/Ray/Screenshot 1.png]]

Deployment is a logical definition of the service. We can assign to a deployment specific amount of resources (CPU, GPU).

There is also created a proxy which receives clients requests and forwards them to a proper replica.

Deployment brings additional functionalities to Ray Core Actor, such as:
- Autoscaling and replication – Set up a number of replicas or allow Ray Serve to automatically scale up / down replicas.
- Request routing – Ray Serve Deployment adds a proxy that routes HTTP/gRPS requests or internal calls (using .remote() in our Python code where we created a Deployment) automatically to replicas.
- HTTP/gRPC Ingress - Can expose REST/gRPC endpoints (via route_prefix or FastAPI integration).
- Fault Tolerance & Lifecycle Management - Serve automatically restarts Deployment replicas if they fail.

More info about Ray Core Actors and Worker processes can be found in the ‘Ray Core > Actors’ section in this document.

#MLEngineering 