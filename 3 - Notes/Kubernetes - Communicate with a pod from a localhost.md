Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
In order to communicate with a pod on a specific port using a specific protocol from a localhost, we can use:
- Port forward ([[Kubernetes - Port foward|link]])
	- It will cause that all the traffic from the localhost will go to the pod
- NodePort service ([[Kubernetes - Service|link]])
	- It will cause that all the traffic from any server will go to the pod