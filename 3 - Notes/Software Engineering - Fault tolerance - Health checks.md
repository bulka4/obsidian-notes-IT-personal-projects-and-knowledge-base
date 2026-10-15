Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Health checks are mechanisms that verify whether a service instance is healthy and able to handle requests.

A system (e.g., load balancer or orchestrator like Kubernetes) periodically asks a service:
> "Are you working correctly?"

Health checks improve fault tolerance by allowing systems to automatically detect unhealthy instances and route traffic to healthy ones.

Common types include liveness and readiness checks - [[Software Engineering - Deployment - Readiness & liveness probes]].