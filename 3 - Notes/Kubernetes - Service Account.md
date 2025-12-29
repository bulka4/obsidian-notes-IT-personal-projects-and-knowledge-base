Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Service Account is a special kind of account used by rpocesses running in pods to interact with the Kubernetes API. It’s like a “user identity” for pods.

**Purpose**
A Service Account provides authentication when Pod wants to read/write Kubernetes resources (e.g., secrets, config maps, jobs).

**Default Service Account**
Every namespace has a default service account. If we don’t specify one, pods automatically use it.

**Custom Service Account**
We can create a service account with specific **roles/permissions** via Role-Based Access Control (RBAC).

For example:

Create a Service Account:
```
apiVersion: v1
kind: ServiceAccount
metadata:
	name: mlflow-sa
	namespace: mlflow
```

Attach it to a Pod or Deployment:
```
spec:
	serviceAccountName: mlflow-sa
```

Assign role to the Service Account:
![[2 - Images/Kubernetes/Screenshot 7.png]]

#Cloud #DevOps #DistributedComputing #DataEngineering 