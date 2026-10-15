Tags: [[__Software_Engineering]]
#SoftwareEngineering  

# Introduction
Resource requests and limits define how much CPU and memory a service expects and is allowed to use.

In this document we will focus on how this works in Kubernetes but this is a general concept.
# Request
A **request** is the amount of resources Kubernetes **reserves/uses when scheduling the pod**.
```
resources:
  requests:
    cpu: "500m"
    memory: "512Mi"
```

Meaning roughly:
> “Schedule this pod on a node that can provide 0.5 CPU and 512 MiB memory.”

It is primarily about **scheduling and guaranteed resource availability**.
# Limit
A **limit** is the maximum amount the container is allowed to consume.
```
resources:
  limits:
    cpu: "1"
    memory: "1Gi"
```

Meaning:
> “This container can use up to 1 CPU and 1 GiB memory.”

If it tries to exceed the limits, Kubernetes/container runtime handles it differently for each resource:
- **CPU:** the container is throttled.
- **Memory:** the container can be killed due to OOM (out of memory).

So:
```
requests                 limits
   ↓                        ↓
"What do I need?"       "What's the maximum?"
   ↓                        ↓
scheduling              resource enforcement
```

Example:
```
resources:
  requests:
    cpu: "500m"
    memory: "512Mi"
  limits:
    cpu: "1"
    memory: "1Gi"
```

This means the pod requests **0.5 CPU / 512 MiB**, but can use up to **1 CPU / 1 GiB**.
