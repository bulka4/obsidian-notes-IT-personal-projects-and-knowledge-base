Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
It is a resource which is the smallest unit in Kubernetes. It is an abstraction of a container. Inside of a Pod we have a container running with app, and that Pod is running on one of the nodes.

We don’t work with the container itself in Kubernetes, just with a Pod or abstractions of Pod (for example Deployment).
# Pod container settings
Here are described settings related to the Pod container:
```
apiVersion: v1
kind: Pod
metadata:
	...
spec:
	containers:
		- name: myapp-container
		  image: myapp:latest
```

## Readiness & Liveness
Liveness probe:
- Checks if a container is alive (not crashed or stucked)
- If the probe fails, Kubernetes restarts the container.
- It prevents a stuck or crashed container from hanging indefinitely.

Readiness probe:
- Checks if a container is ready to serve traffic.
- If the probe fails, Kubernetes removes the Pod from Service endpoints, so no traffic is sent to it.
- It ensures that traffic only goes to fully initialized containers (for example, after DB connections are ready).

We define Liveness and Readiness in a containers specification of a Pod:
![[2 - Images/Kubernetes - Details/Screenshot 1.png]]
