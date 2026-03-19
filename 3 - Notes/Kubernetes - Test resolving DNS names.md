Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
To test resolving DNS names from a pod, we can create a testing pod like described here - [[Kubernetes - Create a pod for debugging and get access to its bash session|link]], we can use for it for example the busybox:1.28 image, and run those commands from the created pod:
```bash
nslookup kubernetes.default # DNS name for API server
nslookup google.com # check a public domain
nslookup <service-name>.<namespace> # domain name for some Kubernetes Service
```
