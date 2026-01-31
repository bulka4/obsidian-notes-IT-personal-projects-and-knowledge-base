Tags: [[_Git]] [[_Kubernetes]]
#Git #Kubernetes 

# Introduction
Git-sync can be enabled for pods using Helm. 
# values.yaml
In the values.yaml we need to include:
```yaml
gitSync:
  enabled: true
  repo: https://github.com/my-org/my-repo.git
  branch: main
  rev: HEAD
  depth: 1
  subPath: ""
  period: 30s

workspace:
  mountPath: /workspace
  
pvc:
  enabled: true
  name: workspace-pvc
  accessMode: ReadWriteOnce
  size: 10Gi
  storageClass: managed-csi
```
# Volume
We need to create a volume which will be mounted to both containers running git-sync and our main app.

Git-sync will be writing pulled code from repo into that volume, our app will be reading it.
```yaml
{{- if .Values.pvc.enabled }}
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: {{ .Values.pvc.name }}
spec:
  accessModes:
    - {{ .Values.pvc.accessMode }}
  resources:
    requests:
      storage: {{ .Values.pvc.size }}
  {{- if .Values.pvc.storageClass }}
  storageClassName: {{ .Values.pvc.storageClass }}
  {{- end }}
{{- end }}
```
# Init container for jobs
When we run our code as a job, we can run git-sync as an init container:
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: example-job
spec:
  template:
    spec:
      restartPolicy: Never
      volumes:
        - name: workspace
          persistentVolumeClaim:
            claimName: workspace-pvc

      initContainers:
        - name: git-sync
          image: registry.k8s.io/git-sync/git-sync:v4.0.0
          env:
            - name: GIT_SYNC_REPO
              value: https://github.com/my-org/my-repo.git
            - name: GIT_SYNC_ONE_TIME
              value: "true"
            - name: GIT_SYNC_ROOT
              value: /workspace
          volumeMounts:
            - name: workspace
              mountPath: /workspace

      containers:
        - name: app
          image: python:3.11
          command: ["python", "/workspace/my-repo/main.py"]
          volumeMounts:
            - name: workspace
              mountPath: /workspace
```
# Deployment
When we run our code as a deployment, we can run git-sync as another, sidecar container in the same pod:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: example
  template:
    metadata:
      labels:
        app: example
    spec:
      volumes:
        - name: workspace
          persistentVolumeClaim:
            claimName: workspace-pvc

      containers:
        - name: git-sync
          image: registry.k8s.io/git-sync/git-sync:v4.0.0
          env:
            - name: GIT_SYNC_REPO
              value: https://github.com/my-org/my-repo.git
            - name: GIT_SYNC_PERIOD
              value: 30s
            - name: GIT_SYNC_ROOT
              value: /workspace
          volumeMounts:
            - name: workspace
              mountPath: /workspace

        - name: app
          image: python:3.11
          command: ["python", "/workspace/my-repo/main.py"]
          volumeMounts:
            - name: workspace
              mountPath: /workspace
```
