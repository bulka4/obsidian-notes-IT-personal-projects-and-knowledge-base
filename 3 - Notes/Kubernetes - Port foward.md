Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Kubernetes port forward command:
```
kubectl port-forward svc/service-name local_port:remote_port
```
can be used to forward all the traffic from the local machine on the `local_port` port to the `remote_port` port of the specified Kubernetes service.

This way we can communicate with pods attached to that service from our local computer, if normal communication over internet is not possible.