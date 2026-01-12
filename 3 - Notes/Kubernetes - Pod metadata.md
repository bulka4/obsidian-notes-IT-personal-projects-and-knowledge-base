Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Every Kubernetes pod ([[Kubernetes - Pod|link]]) has a metadata section with descriptive information about that pod.

There are fields like:
- `name` - Pod's name
- labels - Key-value pairs created in pod's manifest ([[Kubernetes - Manifest|link]])
# Creating metadata
We create metadata in a manifest:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ...
  labels:
    app: ...
```
or
```yaml
spec:
  template:
    metadata:
      labels:
        app: ...
      annotations:
        kubeflow.org/rank: "0"  
```
# Using metadata
We can use read metadata values in a manifest, for example like this:
```yaml
env:
  - name: RANK
    valueFrom:
      fieldRef:
        fieldPath: metadata.annotations['kubeflow.org/rank']
  - name: POD_NAME
    valueFrom:
      fieldRef:
        fieldPath: metadata.name
```
