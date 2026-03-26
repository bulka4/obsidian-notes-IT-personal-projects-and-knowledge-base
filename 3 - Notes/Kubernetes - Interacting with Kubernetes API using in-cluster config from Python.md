Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
As explained here - [[Kubernetes - Interacting with Kubernetes API using in-cluster config|link]], we can interact with Kubernetes API ([[Kubernetes - Components - API server|link]]) (e.g. creating other pods) from a pod.

This document explains how to do this using Python.
# Create configs
Using the `load_incluster_config` function we create configs with credentials used for authentication when making Rest API calls to Kubernetes API:
```python
from kubernetes import config
config.load_incluster_config()
```

It uses files provided in the pod by Kubernetes: `token`, `ca.cert` and `namespace`.
# Create an API client
Once we created configs, we need to create an API client to interact with Kubernetes API:
```python
from kubernetes import client
api = client.CustomObjectsApi()
```

There are different API clients for performing different actions on Kubernetes. For example `client.CustomObjectsApi()` is for creating custom resources and `client.CoreV1Api()` is for creating pods.
# Interact with Kubernetes API
Once we have client prepared, we can use it to interact with Kubernetes API, for example to create a pod:
```python
from kubernetes import client, config

config.load_incluster_config()
api = client.CoreV1Api()

pod = client.V1Pod(
    metadata=client.V1ObjectMeta(name="example-pod"),
    spec=client.V1PodSpec(
        containers=[
            client.V1Container(
                name="nginx",
                image="nginx"
            )
        ]
    )
)

api.create_namespaced_pod(
    namespace="default",
    body=pod
)
```
