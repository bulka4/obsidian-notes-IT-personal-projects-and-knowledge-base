Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Notes
## Helm chart
To deploy Airflow on Kubernetes we use the official Helm chart. It is used as a dependency in the `helm_charts/airflow/Chart.yaml` file and in the same folder Terraform will create the `values.yaml` file.
### values.yaml
The `values.yaml` file will be provided for that chart in the `helm_charts/airflow` folder and it will be created by Terraform.

It interpolates the `terraform/template_files/helm_charts/values-airflow.yaml` template to create it ((inserts variables values into the template file). 
## Git-sync
We use git-sync to pull code from the repo, with Airflow tasks to run, create a volume and mount it into pods created by Airflow where that code runs.

We create a separate PVC which will be used by git-sync to store code there, so we can later use this PVC to mount it to other pods, for example pods created by Airflow for executing tasks using KubernetesPodOperator.

By default, git-sync would create a volume available only for Airflow pods (scheduler etc).
## Airflow logs
Airflow logs are being saved in Azure Storage Account. We configure that in the `values.yaml` file.
### Service Principal
We create a connection which uses credentials of a Service Principal with permissions to connect to Storage Account (it is configured also in the `values.yaml` file)
## Metadata db
We create a PostgreSQL db for Airflow metadata using Airflow Helm chart.

We do this so we don't pay for a managed service but for production it is recommended to use a managed service since running a database on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
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
    version: 1.13.0   
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
## Create PostgreSQL secret
Create a secret with a connection string to PostgreSQL which will be used by Airflow to connect. 

Use this only if deploying PostgreSQL separately (i.e. when the `postgresql.enabled` value in the `values.yaml` is set up to `false`):
```bash
kubectl create secret generic airflow-postgres \
  --from-literal=connection=postgresql+psycopg2://airflow:airflow@postgres-host:5432/airflow \
  -n airflow
```
## Install Airflow
```bash
kubectl create namespace airflow

helm dependency update

helm install airflow ./helm_charts/airflow \
  -n airflow \
  -f values.yaml
```