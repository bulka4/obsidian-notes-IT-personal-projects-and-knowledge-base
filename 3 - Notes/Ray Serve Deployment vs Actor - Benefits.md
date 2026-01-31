Tags: [[__Machine_Learning_Engineering]]
#MLEngineering 

# Introduction
Ray Serve Deployment ([[Ray Serve - Deployment|link]]) brings additional functionalities to Ray Core Actor ([[Ray Core - Actors|link]]), such as:
- Autoscaling and replication – Set up a number of replicas ([[Ray Serve - Replica|link]]) or allow Ray Serve to automatically scale up / down replicas.
- Request routing – Ray Serve Deployment adds a proxy that routes HTTP/gRPS requests or internal calls (using .remote() in our Python code where we created a Deployment) automatically to replicas.
- HTTP/gRPC Ingress - Can expose REST/gRPC endpoints (via route_prefix or FastAPI integration).
- Fault Tolerance & Lifecycle Management - Serve automatically restarts Deployment replicas if they fail.