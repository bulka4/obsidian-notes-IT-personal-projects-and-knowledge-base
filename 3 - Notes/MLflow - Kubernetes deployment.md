Tags: [[__Machine_Learning_Engineering]], [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
This document described how to deploy MLflow on Kubernetes using Helm.
# Notes
## Git-sync
We use git-sync to run code from repo as a MLflow project. It runs in an init container in the job running the MLflow project.
## MySQL as a backend store
We use MySQL as a backend store for MLflow Tracking Server. We deploy it using the official Helm chart, as a dependency in the Chart.yaml file.

For production it is recommended to use a managed MySQL database as running databases on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
## Azure Storage Account as an artifact store
We use an Azure Storage Account as an artifact store.
## ACR
We use an ACR for storing Docker images used to run Kubernetes pods.
# Create secrets
## MySQL secret
Create a secret with credentials to MySQL. That secret will be used when installing the 'MLflow setup' Helm chart:
```bash
kubectl create secret generic mlflow-mysql \
  --from-literal=root_password=XXXX \
  --from-literal=user_password=XXXX \
  -n mlflow
```
## Storage Account secret
Create a secret with an access key to a Storage Account:
```bash
kubectl create secret generic mlflow-sa \
  --from-literal=access_key=XXX\
  -n mlflow
```
## ACR secret
Create a secret with credentials for pulling images from ACR. We can use for that client ID and secret of an Azure Service Principal with the 'acrpush' role:
```bash
kubectl create secret docker-registry acr-secret \
  --namespace mlflow \
  --docker-server=${acr_url} \ # ACR URL (<registry-name>.azurecr.io) 
  --docker-username=${client_id} \
  --docker-password=${client_secret} \
  --docker-email=unused@example.com # It doesn't matter what we put here but it is needed
```
# MLflow setup Helm chart
This section describes Helm chart which is used to perform an initial setup needed for running MLflow projects.

Once we deploy it, we can deploy the second chart for running a MLflow project.
## Docker image
Docker image we will use in the deployment, for running the Tracking Server, is created using the following Dockerfile:
```Dockerfile
# Image for running MLflow Tracking Server. Here we install packages needed to run the Tracking Server which uses Azure Storage Account 
# as an artifact store and MySQL as a backend store.

FROM python:3.9-slim

RUN apt-get update && apt-get install -y \
    build-essential \
    default-libmysqlclient-dev \
    gcc \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

RUN pip install mlflow[extras] azure-storage-blob azure-identity pymysql mysqlclient
```
## Helm chart file structure
Our Helm chart has the following structure:
```
|-- Chart.yaml
|-- values.yaml
|-- templates \
	|-- common\
		|-- acr-secret.yaml
	|-- mlflow_project \
		|-- service-account.yaml
	|-- tracking_server \
		|-- deployment.yaml
		|-- mysql-pvc.yaml
		|-- secret.yaml
		|-- service.yaml
```
## Chart.yaml
```yaml
apiVersion: v2
name: mlflow-setup
description: Helm chart for deploying resources needed for running MLflow projects as Jobs
version: 0.1.0

# Install additional dependencies - Bitnami MySQL. It will be used as a backend store for the MLflow Tracking Server.
dependencies:
  - name: mysql
    version: 14.0.3
    repository: https://charts.bitnami.com/bitnami
```
## values.yaml
```yaml
# General namespace for all resources
namespace: ${namespace}

# Parameters for installing MySQL dependency
mysql:
  fullnameOverride: mysql # Name of the created resource
  primary:
    persistence:
      enabled: true
      existingClaim: mysql-pvc # We will create this volume in this chart as well.
      storageClass: ""
  auth:
    rootPassword:
      secretKeyRef:
	        name: mlflow-mysql
	        key: client_secret
    # Create a new user. This is needed so MLflow Tracking Server can connect
    database: mlflow # DB that will be created
    username: mlflow # custom user
    password: # custom user password
      secretKeyRef:
	        name: mlflow-mysql
	        key: user_password
    
    # rootPassword: abc123
    # # Create a new user. This is needed so MLflow Tracking Server can connect
    # database: mlflow    # DB that will be created
    # username: mlflow    # custom user
    # password: mlflow123 # custom user password

# Storage class for PVC for MySQL backend store. The 'managed-csi' option causes that data will be stored in an Azure Disk. It will be created on 
# demand when creating this volume and deleted when deleting the Volume. It is used in the tracking_server > mysql-pvc.yaml template.
mySqlMounting:
  storageClass: managed-csi

# MLflow configuration. Here we have the following values:
# - trackingServerSecretName - Name of the secret with values used by the Tracking Server to connect to the backend and artifact store
# - serviceAccountName - Name of the Service Account used in the Job running the MLflow project
# - trackingServerServiceName - Name of the Service which Tracking Server deployment will be using
# - Parameters related to the Azure Storage Account which will serve as an artifact store:
#   - azureConnectionString - Connection string to the Storage Account. It will be stored in the trackingServerSecretName secret.
#   - mlflowStorageAccountName - Name of the Storage Account. Used in the Tracking Server Deployment.
#   - mlflowContainerName - Name of the container in the Storage Account which will be used. Used in the Tracking Server Deployment.
mlflow:
  trackingServerSecretName: mlflow-ts-secret
  serviceAccountName: ${service_account_name}
  trackingServerServiceName: ${tracking_server_service_name}
  azureConnectionString: DefaultEndpointsProtocol=https;AccountName=${mlflow_storage_account_name};AccountKey=${mlflow_storage_account_access_key};EndpointSuffix=core.windows.net
  mlflowStorageAccountName: ${mlflow_storage_account_name}
  mlflowContainerName: ${mlflow_container}

# Information about ACR and images it contains:
#   - URL - ACR URL (<registry-name>.azurecr.io)
#   - trackingServerImageName - Name of the image used for the MLflow Tracking Server
#   - secretName - Name of the secret used for authentication when accessing ACR. 
acr:
  url: ${acr_url}
  trackingServerImageName: ${tracking_server_image_name}
  secretName: ${acr_secret_name}
```
## MLflow project
### Service account
mlflow_project/service-account.yaml:
```yaml
# This Service Account will be used when we run a MLflow project using the mlflow_project chart for authentication when reading a secret used to pull an image from ACR.
# We will assign to is a proper role in the service-account-role-binding.yaml template.

apiVersion: v1
kind: ServiceAccount
metadata:
  name: {{ .Values.mlflow.serviceAccountName }}
  namespace: {{ .Values.namespace }}
imagePullSecrets:
- name: {{ .Values.acr.secretName }}
---
# Assign to the Service Account a role allowing for reading secrets (it will read the secret for connecting to ACR)

apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: secret-reader
  namespace: {{ .Values.namespace }}
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: secret-reader-binding
  namespace: {{ .Values.namespace }}
subjects:
- kind: ServiceAccount
  name: {{  .Values.mlflow.serviceAccountName }}
  namespace: {{ .Values.namespace }}
roleRef:
  kind: Role
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```
## Tracking server
### Deployment
tracking_server/deployment.yaml:
```yaml
# Deployment for running MLflow Tracking Server.

apiVersion: apps/v1
kind: Deployment
metadata:
  name: mlflow-server
  namespace: {{ .Values.namespace }}
  labels:
    app: mlflow
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mlflow
  template:
    metadata:
      labels:
        app: mlflow
    spec:
      # Get a secret with value for authentication to the ACR.
      imagePullSecrets:
        - name: {{ .Values.acr.secretName }}
      containers:
      - name: mlflow
        image: "{{ .Values.acr.url }}/{{ .Values.acr.trackingServerImageName }}"
        ports:
        - containerPort: 5000
        env:
        # Create environment variables with values from the secret created as well in this chart. They will be used by the
        # MLflow Tracking Server for authentication when connecting to the artifact store (Storage Account) and backend store (MySQL).
        - name: AZURE_STORAGE_CONNECTION_STRING
          valueFrom:
            secretKeyRef:
              name: {{ .Values.mlflow.trackingServerSecretName }}
              key: AZURE_STORAGE_CONNECTION_STRING
        - name: DB_URI
          valueFrom:
            secretKeyRef:
              name: {{ .Values.mlflow.trackingServerSecretName }}
              key: DB_URI
        # Run the command to start the Tracking Server
        command: ["mlflow"]
        args:
          [
            "server",
            "--host", "0.0.0.0",
            "--port", "5000",
            "--backend-store-uri", "$(DB_URI)",
            "--artifacts-destination", "wasbs://{{ .Values.mlflow.mlflowContainerName }}@{{ .Values.mlflow.mlflowStorageAccountName }}.blob.core.windows.net/"
          ]
```
### MySQL PVC
tracking_server/mysql-pvc.yaml:
```yaml
# When installing MySQL chart with Helm we will use the following Volume Claim (it will be used by MySQL Pod)

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: {{ .Values.mysql.primary.persistence.existingClaim }}
  namespace: {{ .Values.namespace }}
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: {{ .Values.mySqlMounting.storageClass }}
  resources:
    requests:
      storage: 8Gi
```
### Secret (to delete)
tracking_server/secret.yaml:
```yaml
# Create a secret with values for accessing the Azure Blob Storage and MySQL.
# This secret will be used when deploying MLflow Tracking Server.

apiVersion: v1
kind: Secret
metadata:
  name: {{ .Values.mlflow.trackingServerSecretName }}
  namespace: {{ .Values.namespace }}
type: Opaque
stringData:
  AZURE_STORAGE_CONNECTION_STRING: {{ .Values.mlflow.azureConnectionString }}
  DB_URI: "mysql://{{ .Values.mysql.auth.username }}:{{ .Values.mysql.auth.password }}@{{ .Values.mysql.fullnameOverride  }}.{{ .Values.namespace }}.svc.cluster.local:3306/{{ .Values.mysql.auth.database }}"
```
### Service
tracking_server/service.yaml:
```yaml
# A Service used by the MLflow Tracking Server Deployment

apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.mlflow.trackingServerServiceName }}
  namespace: {{ .Values.namespace }}
spec:
  type: LoadBalancer  # Or use Ingress
  # type: ClusterIP # ClusterIP will be only for connectivity from inside of the cluster
  selector:
    app: mlflow
  ports:
  - port: 5000
    targetPort: 5000
```
# MLflow project Helm chart
The MLflow project Helm chart is used to run a MLflow project using infrastructure prepared by the MLflow setup Helm chart described earlier.
## Docker image
Docker image we will use in the job running the MLflow project is created using the following Dockerfile:
```Dockerfile
# Image for running the MLflow project

FROM python:3.11-slim

# Install sh and git:
# - sh: Needed because when deploying a Job running MLflow project, we execute the command "sh -c "mlflow run ...""
# - git: Required to run a MLflow project
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    dash \
    && rm -rf /var/lib/apt/lists/*

# Copy and install Python libraries used in the MLflow project
COPY mlproject_requirements.txt /root/requirements.txt

RUN pip install -r /root/requirements.txt
```
## Helm chart file structure
```
|-- Chart.yaml
|-- values.yaml
|-- templates /
	|-- _helpers.tpl
	|-- job.yaml
```
## Chart.yaml
This file is only descriptive:
```yaml
apiVersion: v2
name: mlflow-project-job
description: Helm chart for running a MLflow project in a local mode as a Job.
version: 0.1.0
```
## values.yaml
```yaml
namespace: ${namespace}
serviceAccountName: ${service_account_name}
image: ${acr_url}/${mlproject_image_name}

# Command to execute of the format: "mlflow run <path> -e <entrypoint-name> --<param1> <value1> --env-manager local"
# - <path> - Path to the MLflow project to run. File share in Azure Storage Account will be mounted to the Job on path
#             Specified in the 'mountPath' parameter in Job's manifest. So if mountPath = /mnt/mlprojects and project is
#             the File share at the mlflow_project path, then the <path> parameter here is /mnt/mlprojects/mlflow_project.
# - <entrypoint-name> - Name of the entrypoint from the MLproject file to run
# - <param1>, <value1> - Parameter with a value for the entrypoint
# - "--env-manager local" - Indicates to use the local environment. We want to use it because in the Docker image which we
#                           are using in the Job already contains prepared environment for running the MLflow project.
# - --experiment-name - Indicates which experiment assign this run to.
command: "mlflow run /mnt/mlprojects/mlflow_project -e train --env-manager local --experiment-name=lasso_test"

# MLflow server URI. It uses DNS name assigned by the Service linked to the Tracking Server deployment.
mlflowTrackingUri: http://${tracking_server_service_name}.${namespace}.svc:5000

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
## \_helpers.tpl
This value makes sure that each deployed job, which runs a MLflow project, will have a unique name:
```tpl
{{- define "mlflow-job.fullname" -}}
{{- printf "%s-%s" .Release.Name .Chart.Name | trunc 63 | trimSuffix "-" -}}
{{- end }}
```
## Volume
We need to create a volume which will be mounted to both containers running git-sync and MLflow project.

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
## job.yaml
Job running the MLflow project:
```yaml
# Job for running a MLflow project.

apiVersion: batch/v1
kind: Job
metadata:
  name: {{ include "mlflow-job.fullname" . }} # Unique name for the Job using the Chart name and Release name
  namespace: {{ .Values.namespace }}
spec:
  ttlSecondsAfterFinished: 3600
  backoffLimit: 2
  template:
    spec:
      # Service Account used for reading a secret for accessing an image from ACR.
      serviceAccountName: {{ .Values.serviceAccountName }}
      
      volumes:
      - name: workspace
        persistentVolumeClaim:
          claimName: {{ .Values.pvc.name }}
      
      # Init container which will run git-sync
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
	      - name: mlflow-job
	        image: {{ .Values.image }}
	        # Command to run a MLflow project
	        command: ["sh", "-c"]
	        args: 
	          - {{ .Values.command }}
	        env:
	        # Set up MLFLOW_TRACKING_URI env variable indicating URI of the Tracking Server to connect to.
	        - name: MLFLOW_TRACKING_URI
	          value: {{ .Values.mlflowTrackingUri }}
	        volumeMounts:
		        # Mount a volume with MLflow project script pulled from the repo by git-sync
		        - name: workspace
		          mountPath: /mnt/mlprojects
      restartPolicy: Never
```