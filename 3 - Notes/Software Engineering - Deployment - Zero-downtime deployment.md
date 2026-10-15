Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Zero-downtime deployment means deploying a new version of a service without making the service unavailable to users.

We do this by:
- running a service using multiple replicas (e.g. running in different Kubernetes pods)
- starting a new version of a service as a new replica 
- once a new version replica is ready, we gracefully shutdown old replicas.

