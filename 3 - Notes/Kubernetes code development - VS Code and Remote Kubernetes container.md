Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Using VS Code + a Kubernetes container lets us to connect to a Kubernetes pod, edit files inside, run and debug code from our local computer. 

It doesn't make automatically our local code available in the pod, we need to provide it separately. We can for example clone a git repo (we can do that from VS code terminal).

It uses the same configuration as `kubectl` (kubeconfig file) uses to connect to the Kubernetes cluster.
# Setup
## VS extensions
Install these extensions in VS Code:
- Remote Development
- Kubernetes
## Development image
Prepare an image for development, for example:
```dockerfile
FROM python:3.11  
  
WORKDIR /workspace  
  
RUN pip install numpy pandas scikit-learn jupyter  
  
CMD ["sleep", "infinity"]
```
## Dev pod
Prepare a dev pod on Kubernetes using prepared image. Optionally we can use PV to store code in an external storage, so we don't loose it when pod dies. 

We can prepare a Helm chart like this:
```bash
|-- Chart.yaml
|-- values.yaml
|-- templates/
	|-- pod.yaml
	|-- pvc.yaml
```

`pod.yaml`:
```YAML
apiVersion: v1
kind: Pod
metadata:
  name: dev-pod
  namespace: {{ .Values.namespace }}
spec:
    containers:
      - name: dev
        image: {{ .Values.image }}
        command: ["sleep", "infinity"]
      volumeMounts:
        - name: code
          mountPath: {{ .Values.mountPath }}
    volumes:
      # PV with code to develop
      - name: code
        persistentVolumeClaim:
        claimName: code-pvc
```

`pvc.yaml`:
```yaml
# This is a PVC used to store code we develop in the pod. It stores data on the localhost (the hostPath parameter).
# It can be changed to use Azure File share as data storage (commented code). It supports ReadWriteMany access mode
# so this PV can be mounted into many pods on different nodes.

apiVersion: v1
kind: PersistentVolume
metadata:
  name: code-pv
  namespace: {{ .Values.namespace }}
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: {{ .Values.hostPath }}
  # csi:
  #   driver: file.csi.azure.com  # Driver for Azure File Share
  #   volumeHandle: "{{ .Values.storageAccountName }}#{{ .Values.fileShareName }}""
  #   volumeAttributes:
  #     shareName: {{ .Values.fileShareName }}
  #     storageAccount: {{ .Values.storageAccountName }}
  #   # Secret with the following keys:
  #   #   - azurestorageaccountname - Storage Account name
  #   #   - azurestorageaccountkey - Access key
  #   nodeStageSecretRef:
  #     name: {{ .Values.secretName }}
  #     namespace: {{ .Values.namespace }}
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: code-pvc
  namespace: {{ .Values.namespace }}
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: ""
  resources:
    requests:
      storage: 1Gi
  volumeName: code-pv
```

`Chart.yaml`:
```yaml
apiVersion: v2
name: dev-pod
description: Pod for code development
type: application
version: 0.1.0
appVersion: "3.1.3"
```

`values.yaml`:
```yaml
# namespace where to create the pod
namespace: mlflow
# Docker image to use
image: mlflow-project
# Path at the host where to store PV's data (when using kind, this is the extraMounts.containerPath parameter from the kind-config.yaml file)
hostPath: /git_code
# Path in the pod where we will keep developed code (PV with code will be mounted there)
mountPath: /root
```

Install:
```bash
helm -n <namespace> install dev-pod .
```
## Kubeconfig file
We need to have properly configured the kubeconfig file (usually saved at `/user/.kube/config`). This is the same config file used by `kubectl` to interact with Kubernetes. 

It is used by VS Code to connect to the Kubernetes cluster.
### Local Kubernetes cluster
If we run a Kubernetes cluster on our local computer using for example kind, then in the kubeconfig file, in the `clusters.cluster_name.server` field we need to have `127.0.0.1` as IP address, not `0.0.0.0`
## Attach VS Code to the Kubernetes container
- In VS Code, click on the Kubernetes extension (Kubernetes icon on the left-hand side panel)
- In the clusters section, click on our cluster
- Click on namespaces, right click on our chosen namespace and click on the 'use namespace'
- Click on workloads > pods, right click on the chosen pod and click on the 'attach VS code'
## Sync local code
We need to make our local code available in the pod. Then we will be using our local VS code to edit it and run in a pod.

We can for example use git to clone the code into the pod (we can clone it from VS code since it is connected).