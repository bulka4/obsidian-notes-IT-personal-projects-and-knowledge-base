Tags: [[_My_projects]]
#MyProjects 

# Introduction
We can use VS Code Kubernetes extension to get access to the pod's filesystem. We can edit files and run shell commands.

More info about it can be found here - [[Kubernetes code development - VS Code and Remote Kubernetes container]]
## Setup
### VS extensions
Install these extensions in VS Code:
- Remote Development
- Kubernetes
### Modify kubeconfig file
Kubeconfig file (usually located at `C:\Users\username\.kube\config`) is used by VS code to connect to Kubernetes.

We need to modify it and change the IP address from `0.0.0.0` to `127.0.0.1` in the `clusters.cluster_name.server` field, for the kind cluster.
### Run the dev pod
Run the pod into which we want to connect and inside of which we want to develop code. We can use for that for example the `helm_charts/development_pod` Helm chart. In the `values.yaml` we can specify what image we want to use.

Install it:
```bash
# execute below command from the helm_charts/development_pod folder
helm -n <namespace> install dev-pod . &
```
### Attach VS Code to the Kubernetes container
- In VS Code, click on the Kubernetes extension (Kubernetes icon on the left-hand side panel)
- In the clusters section, click on our cluster
- Click on namespaces, right click on our chosen namespace and click on the 'use namespace'
- Click on workloads > pods, right click on the chosen pod and click on the 'attach VS code'
### Sync local code
We need to make our local code available in the pod. Then we will be using our local VS code to edit it and run in a pod.

We can for example use git to clone the code into the pod (we can clone it from VS code since it is connected).
### PV storage
In the `helm_charts/development_pod` Helm chart, we use a PV for storing code we develop in the pod. 

When using kind, we use the localhost for storing data. By default, the `git_code` folder from the repo root is used as a storage for that PV (we need to create that folder and move there all the files we want).