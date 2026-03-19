Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When we create a service and attach a pod to it, then when we run:
```bash
kubectl get endpoints <service-name> -n <namespace>
```
we will see something like:
```bash
NAME             ENDPOINTS                                         AGE
<service-name>   <ip-address-1>:<port-1>,<ip-address-2>:<port-2>   5s
```
This output shows which IP addresses and ports are attached to a given service name (those are IP addresses of attached pods and open ports).