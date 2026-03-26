Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When we create a pod in Kubernetes with a service account, Kubernetes prepares objects in that pod (files and env vars) which can be used to interact with Kubernetes API ([[Kubernetes - Components - API server|link]]) from that pod, for example to create other pods.
# Explanation
To interact with Kubernetes, for example to create a pod, we need to make a Rest API call to Kubernetes API server.

When we create a pod with a service account, Kubernetes automatically mounts a volume at:
```bash
/var/run/secrets/kubernetes.io/serviceaccount/
```
Inside that directory we have:
```bash
token # JWT token (authentication)  
ca.crt # cluster CA certificate  
namespace # current namespace
```

Those files are used for authentication when making Rest API calls to Kubernetes API server.

Kubernetes also sets up in that pod env vars:
```bash
KUBERNETES_SERVICE_HOST  
KUBERNETES_SERVICE_PORT
```

We can make Rest API calls to Kubernetes API server using this URL:
```bash
https://$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT
```

The service account used in the pod specifies permissions, what we can do from that pod, what operations we can perform and on which types of resource (e.g. creating other pods or deleting secrets).