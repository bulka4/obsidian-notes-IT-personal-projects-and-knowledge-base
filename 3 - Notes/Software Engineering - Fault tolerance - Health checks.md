Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Health checks are mechanisms that verify whether a service instance is healthy and able to handle requests.

A system (e.g., load balancer or orchestrator like Kubernetes) periodically asks a service:
> "Are you working correctly?"

Health checks improve fault tolerance by allowing systems to automatically detect unhealthy instances and route traffic to healthy ones.
# Common types:
1. **Liveness check**
    - "Is the process alive?"
    - If it fails, the system may restart the service.
2. **Readiness check**
    - "Is the service ready to receive traffic?"
    - If it fails, the service stays running but is removed from traffic.