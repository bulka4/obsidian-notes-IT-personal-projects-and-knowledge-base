Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Important concepts
- **Scaling** ([[Software Engineering - Deployment - Scaling|link]]) - increasing a system's ability to handle more workload. There are two types:
	- Vertical scaling (scale up) - Increase the resources of a single machine (CPU, RAM etc.).
	- Horizontal scaling (scale out) - Add more instances of the application
- **Graceful shutdown** ([[Software Engineering - Deployment - Graceful shutdown|link]]) - stopping a service in an orderly way instead of killing it immediately.
- **Zero-downtime deployment** ([[Software Engineering - Deployment - Zero-downtime deployment|link]]) - deploying a new version of a service without making the service unavailable to users. We do this by:
	- running a service using multiple replicas (e.g. running in different Kubernetes pods)
	- starting a new version of a service as a new replica 
	- once a new version replica is ready, we gracefully shutdown old replicas.
- **Deployment rollback** ([[Software Engineering - Deployment - Deployment rollback|link]]) - reverting a deployment of a service to a previous known version when the new version has a problem.
- **Resource requests and limits** ([[Software Engineering - Deployment - Resource requests and limits|link]]) - define how much CPU and memory a service expects and is allowed to use.
- **Autoscaling** ([[Software Engineering - Deployment - Autoscaling|link]]) - a technique of automatically adjusting the amount of computing resources allocated to a workload according to its current or expected demand.
# Deployment strategies
- Rolling deployment ([[Software Engineering - Deployment strategies - Rolling deployment|link]]) - A rolling deployment means updating an application gradually, replacing old instances/pods with new ones gradually instead of replacing everything at once.
- Blue-green deployment ([[Software Engineering - Deployment strategies - Blue-green deployment|link]]) - deployment strategy where we run the two versions simultaneously
- Canary deployment ([[Software Engineering - Deployment strategies - Canary deployment|link]]) - deployment strategy where we send only a small portion of traffic to the new version initially
- Recreate deployment ([[Software Engineering - Deployment strategies - Recreate deployment|link]]) - deployment strategy where we stop the old version and then start the new one
# Related topics
1. [[Software Engineering - Deployment - Scaling]]
2. [[Software Engineering - Deployment - Readiness & liveness probes]]
3. [[Software Engineering - Deployment - Graceful shutdown]]
4. [[Software Engineering - Deployment - Zero-downtime deployment]]
5. [[Software Engineering - Deployment - Deployment rollback]]
6. [[Software Engineering - Deployment - Resource requests and limits]]
7. [[Software Engineering - Deployment - Autoscaling]]
8. [[Software Engineering - Deployment - Deployment strategies]]
	1. [[Software Engineering - Deployment strategies - Rolling deployment]]
	- [[Software Engineering - Deployment strategies - Blue-green deployment]]
	- [[Software Engineering - Deployment strategies - Canary deployment]]
	- [[Software Engineering - Deployment strategies - Recreate deployment]]