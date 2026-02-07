Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Notes
## Helm chart
To deploy Airflow on Kubernetes we use the official Helm chart. It is used as a dependency in the `helm_charts/airflow/Chart.yaml` file and in the same folder Terraform will create the `values.yaml` file.
### values.yaml
The `values.yaml` file will be provided for that chart in the `helm_charts/airflow` folder and it will be created by Terraform.

It interpolates the `terraform/template_files/helm_charts/values-airflow.yaml` template to create it ((inserts variables values into the template file). 
## Git-sync
We use git-sync to pull code from a repo. That code will be available in pods running Airflow components (scheduler etc) and also in pods running tasks created using KubernetesExecutor and KubernetesPodOperator.

git-sync runs in a separate pod, pulls code from repo and saves it in a persistent volume. Then we can mount that volume to other pods to make the code available.

More details about how git-sync works can be found here - [[Git-sync - Kubernetes deployment]].
### File Share
Persistent volume, mounted into the pod running git-sync, into which pulled code is being saved, stores that code in Azure File Share.

We do this because File Share supports RWX (ReadWriteMany) access mode, so we can use that volume for read/write in many pods running on many nodes.

Kubernetes secret with an access key to the Storage Account with that File Share is used for accessing it.
## Airflow logs
Airflow logs are being saved in Azure Storage Account. We configure that in the `values.yaml` file.
### Service Principal
We create a connection which uses credentials of a Service Principal with permissions to connect to Storage Account (it is configured also in the `values.yaml` file)
## Metadata db
We create a PostgreSQL db for Airflow metadata using Airflow Helm chart.

We do this so we don't pay for a managed service but for production it is recommended to use a managed service since running a database on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
## Service account
We create a service account which will be used by Airflow pods for creating new pods where tasks will be executed. 

In that service account we specify what secret will be used in created pods for authentication when pulling an image.
# Kubernetes deployment step by step
## Push Airflow image to ACR
We prepare our own custom Airflow image:
```bash
FROM apache/airflow:2.8.1

RUN pip install \
	apache-airflow-providers-microsoft-azure # To use the connection to Storage Account to save logs there
```
And we push it to ACR.
## Helm chart file structure
We create a Helm chart with the following file structure:
```
|-- Chart.yaml
|-- values.yaml
|-- templates \
	|-- dags-pvc.yaml
	|-- postgresql-service.yaml
	|-- postgresql.yaml
	|-- role-binding.yaml
```
### Chart.yaml
In the `Chart.yaml` file, we use the official Airflow chart as a dependency:
```yaml
apiVersion: v2
name: Airflow
description: Helm chart for deploying Airflow
version: 0.1.0

dependencies:
  - name: airflow
    version: 1.18.0   
    repository: https://airflow.apache.org
```
### values.yaml
```yaml
executor: KubernetesExecutor

airflow:
  image:
    repository: <image_url>
    tag: <tag>
  config:
    AIRFLOW__CORE__LOAD_EXAMPLES: "false"
    AIRFLOW__KUBERNETES__NAMESPACE: airflow
    # Saving logs to Azure Storage Account
    AIRFLOW__LOGGING__REMOTE_LOGGING: "True"
    AIRFLOW__LOGGING__REMOTE_BASE_LOG_FOLDER: "wasb://<container-name>@<storage-account-name>.blob.core.windows.net"
    AIRFLOW__LOGGING__REMOTE_LOG_CONN_ID: "azure_blob" # ID of the connection used for accessing Azure Storage Account for saving Airflow logs

dags:
  # Use git-sync to run code from a repo as tasks in pods created by Airflow
  gitSync:
    enabled: true
    repo: https://github.com/your-org/airflow-dags.git
    branch: main
    subPath: dags
    persistence:
      enabled: true
      existingClaim: airflow-dags-pvc

# Create a PostgreSQL for Airflow metadata
postgresql:
  enabled: true

# Use the below configuration if we use an external PostgreSQL db, not the one created in this chart by setting
# postgresql.enabled = true in this file.
# data:
#   # Use the secret with the connection string to Postgres which will be used by Airflow to connect.
#   metadataSecretName: airflow-postgres
  
# Connection for accessing Azure Storage Account for saving Airflow logs. Values are taken from Kubernetes secret.
extraConnections:
  - id: azure_blob
    type: wasb
    login: 
		secretKeyRef:
	        name: airflow-azure-blob
	        key: client_id
    password:
	    secretKeyRef:
	        name: airflow-azure-blob
	        key: client_secret
    extra: |
      {
        "tenant_id": "{{ .Values.secrets.tenant_id }}",
        "account_name": "{{ .Values.secrets.account_name }}"
      }
      
# If that doesn't work we can try to use this:
# extra:
#   tenant_id:
#	 secretKeyRef:
#	   name: airflow-azure-blob
#	   key: tenant_id
#   account_name:
#	 secretKeyRef:
#	   name: airflow-azure-blob
#	   key: account_name

secrets:
  tenant_id:
    secretKeyRef:
      name: airflow-azure-blob
      key: tenant_id
  account_name:
    secretKeyRef:
      name: airflow-azure-blob
      key: account_name
```

where we need to provide:
- `<image_url` - URL of our Airflow image in a container registry
- `<tag>` - Tag of the image
- `<storage-account-name>` - Name of the Storage Account for Airflow logs
- `<container-name>` - Name of the container for Airflow logs in Storage Account
### DAGs PVC
dags-pvc.yaml:
```yaml
# This is a PVC used to store code pulled from a repo by git-sync.

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: airflow-dags-pvc
  namespace: airflow
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: managed-csi  # Use Azure disk for data storage
  resources:
    requests:
      storage: 5Gi
```
### PostgreSQL
Deployment running PostgreSQL which will be used as Airflow metadata db:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: airflow-postgres
  namespace: airflow
spec:
  replicas: 1
  selector:
    matchLabels:
      app: airflow-postgres
  template:
    metadata:
      labels:
        app: airflow-postgres
    spec:
      containers:
        - name: postgres
          image: public.ecr.aws/bitnami/postgresql:16
          env:
            - name: POSTGRES_USER
              valueFrom:
                secretKeyRef:
                  name: airflow-postgres
                  key: postgres_user
            - name: POSTGRES_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: airflow-postgres
                  key: postgres_password
            - name: POSTGRES_DB
              valueFrom:
                secretKeyRef:
                  name: airflow-postgres
                  key: postgres_database
          ports:
            - containerPort: 5432
          volumeMounts:
            - name: pgdata
              mountPath: /bitnami/postgresql
      volumes:
        - name: pgdata
          emptyDir: {}
```
### PostgreSQL service
Service for PostgreSQL:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: airflow-postgres
  namespace: airflow
spec:
  selector:
    app: airflow-postgres
  ports:
    - protocol: TCP
      port: 5432
      targetPort: 5432
  type: ClusterIP
```
### Role binding
Role binding assigning role to the airflow scheduler service account granting permissions for creating pods, so we can use the KubernetesExecutor which creates a new pod for each Airflow task.

We use here `imagePullSecrets` to specify what secret will be used by pods created by Airflow to pull images from ACR:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: airflow
  name: airflow-scheduler-pod-manager
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["create", "get", "list", "watch", "delete"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: airflow-scheduler-pod-manager-binding
  namespace: airflow
# Pods created using this Service Account will use this secret for pulling images from ACR
imagePullSecrets:
  - name: {{ .Values.acr.secretName }}
subjects:
  - kind: ServiceAccount
    name: airflow-scheduler
    namespace: airflow
roleRef:
  kind: Role
  name: airflow-scheduler-pod-manager
  apiGroup: rbac.authorization.k8s.io
```
## Create a secret for Storage Account
Create a secret with credentials of a Service Principal used for authentication when accessing Azure Storage Account where logs will be saved.

That Service Principal needs to have permissions for accessing Storage Account:
```bash
kubectl create secret generic airflow-azure-blob \
  --from-literal=client_id=<client-id> \
  --from-literal=client_secret=<client-secret> \
  --from-literal=tenant_id=<tenant-id> \
  --from-literal=account_name=<storage-account-name> \
  -n airflow
```

where:
- `<client-id>` - Service Principal client ID
- `<client-secret>` - Service Principal secret
- `<tenant-id>` - Azure tenant ID
- `<storage-account-name>` - Our Storage Account name where to save Airflow logs
## Create PostgreSQL secrets
Create a secret with a connection string to PostgreSQL which will be used by Airflow to connect. 

Use this only if deploying PostgreSQL separately (i.e. when the `postgresql.enabled` value in the `values.yaml` is set up to `false`).

Create a secret used by Airflow:
```bash
kubectl create secret generic airflow-postgres-connection \
	--from-literal=connection=postgresql://airflow:airflow@airflow-postgres:5432/airflow \
	-n airflow
```

Create a secret used by PostgreSQL deployment:
```bash
kubectl create secret generic airflow-postgres \
	--from-literal=postgres_user=airflow \
	--from-literal=postgres_password=airflow \
	--from-literal=postgres_database=airflow \
	-n airflow
```
## Install Airflow
```bash
kubectl create namespace airflow

# Execute below commands from the folder with the Helm chart
helm dependency update

helm install airflow . \
  -n airflow \
  -f values.yaml &
```
# To do
## webserver URL env var
Either update webserver URL env var after installation or create an ingress. Start with the first option (simpler), if it works, then check an ingress option.
### Update after chart installation
Update webserver URL in pods after installation:
```bash
kubectl -n airflow exec -it airflow-webserver -- /bin/bash
AIRFLOW__WEBSERVER__BASE_URL="http://<webserver_service_external_ip"
```
### Create an ingress
I can create ingress in values.yaml:
```yaml
webserver:
  ingress:
    enabled: true
    ingressClassName: nginx   # or azure/application-gateway
    hosts:
      - name: airflow.example.com
        path: /
    tls:
      enabled: true
      secretName: airflow-tls
  config:
    AIRFLOW__WEBSERVER__BASE_URL:
      value: "https://airflow.example.com"
```

or use nginx ingress controller:
```bash
kubectl get pods -n ingress-nginx # check if it already exists
helm install ingress-nginx ingress-nginx/ingress-nginx # install
kubectl get ingress # get address
```