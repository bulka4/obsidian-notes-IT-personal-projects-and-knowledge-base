Tags: [[__Data_Engineering]], [[__Distributed_computing]] [[_Spark]]
#DataEngineering #DistributedComputing #Spark 

# Introduction
This document describes how to set up Spark Thrift Server ([[Spark Thrift Server|link]]) on Kubernetes using a custom Helm chart.

Key features:
- External Hive Metastore (a separate deployment)
	- A separate PostgreSQL as metadata db used by Hive
- Azure Storage Account is used for storing data used for Spark calculations (including storing managed tables' data)
# Notes
## External Hive Metastore
We use an external Hive Metastore (running as a separate deployment) which has benefits as described here - [[Spark Thrift Server - External Hive Metastore benefits|link]].
## Data storage
We store data used for Spark calculations (including managed tables' data) in Azure Storage Account.
## PostgreSQL
PostgreSQL used as a metadata db for Hive Metastore is deployed as a dependency in this Helm chart using the official PostgreSQL Helm chart.

For production it is recommended to use a managed PostgreSQL as running databases on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
### PVC
By default, the official PostgreSQL Helm chart creates a PVC. On AKS, that PVC will use an Azure disk by default.
# Kubernetes deployment
## Build Spark image with Thrift support
Build a Docker image with:
- Spark built with Hive support
- `spark-hive` JARs

Dockerfile used for building the image:
```dockerfile
FROM apache/spark:3.5.0

# Azure storage support (enables reading and saving data in a Storage Account)
RUN curl -o /opt/spark/jars/hadoop-azure-3.3.4.jar \
    https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-azure/3.3.4/hadoop-azure-3.3.4.jar && \
    curl -o /opt/spark/jars/azure-storage-blob-12.22.2.jar \
    https://repo1.maven.org/maven2/com/azure/azure-storage-blob/12.22.2/azure-storage-blob-12.22.2.jar

# PostgreSQL JDBC driver (for connecting to PostgreSQL)
RUN curl -o /opt/spark/jars/postgresql-42.7.1.jar \
    https://repo1.maven.org/maven2/org/postgresql/postgresql/42.7.1/postgresql-42.7.1.jar
```
## Create secrets
### Spark
Create a secret with Service Principal's credentials which will be used in the `spark-defaults.conf` file. Those values will be used to get access to data in the Storage Account.

Values from that secret will be passed into environment variables in the Thrift Server deployment and inserted automatically by Spark into the `spark-defaults.conf` file:
```bash
kubectl create secret generic adls-sp-secret \
  --from-literal=client-id=XXXX \
  --from-literal=client-secret=XXXX \
  --from-literal=tenant-id=XXXX \
  -n spark
```
### Hive Metastore
Secret for Hive Metastore for accessing PostgreSQL metadata db:
```bash
kubectl create secret generic hive-metastore-db-secret \
  --from-literal=hive-password=hivepassword \
  --from-literal=postgres-password=adminpassword \
  -n spark
```
### ACR
Create a secret with credentials for pulling images from ACR. We can use for that client ID and secret of an Azure Service Principal with the 'acrpush' role:
```bash
kubectl create secret docker-registry acr-secret \
  --namespace <namespace> \
  --docker-server=${acr_url} \ # ACR URL (<registry-name>.azurecr.io) 
  --docker-username=${client_id} \
  --docker-password=${client_secret} \
  --docker-email=unused@example.com # It doesn't matter what we put here but it is needed
```
## Helm chart
### Helm chart file structure
We will deploy Spark Thrift Server using our own Helm chart with the following file structure:
```
|-- Chart.yaml
|-- values.yaml
|-- templates \
	|-- _helpers.tpl
	|-- spark-configuration-configmap.yaml
	|-- service-account.yaml
	|-- deployment-thrift-server.yaml
	|-- deployment-hive-metastore.yaml
	|-- service-hive-metastore.yaml
	|-- service-thrift-server.yaml
```
### Chart.yaml
- Install PostgreSQL as a dependency using the official Helm chart which will serve as metadata db for Hive Metastore
```yaml
apiVersion: v2
name: spark-thrift-server
description: Spark Thrift Server with Hive Metastore with PostgreSQL backend
type: application
version: 0.1.0
appVersion: "3.1.3"

dependencies:
  # Install PostgreSQL Helm chart which will serve as metadata db
  - name: postgresql
    version: 15.5.21
    repository: https://charts.bitnami.com/bitnami
```
### values.yaml
```yaml
# Variables for Spark Thrift Server
spark:
  # URL of the Spark Docker image from a container registry
  sparkImageUrl: <your-image-url>
  # Storage Account and container for storing data used by Spark
  storageAccountName: <our-storage-account-name>
  containerName: <our-container-name>

# Variables for Hive Metastore
hive:
  image:
    repository: apache/hive
    tag: 3.1.3
    pullPolicy: IfNotPresent
  metastorePort: 9083
  # Name of the database in PostgreSQL db with metadata and name of the user who is the owner of that database
  database:
    name: hive
    user: hive

# Variables for PostgreSQL which will be used as Hive Metastore metadata db
postgresql:
  auth:
    username: hive # Set up the POSTGRES_USER env var (user who is an owner of the created database)
    database: hive # Set up the POSTGRES_DB env var (name of the created database)
    # Set up passwords from the secret
    existingSecret: hive-metastore-db-secret # Name of the secret
    secretKeys:
      adminPasswordKey: postgres-password # Set up POSTGRES_POSTGRES_PASSWORD env var (password for the `postgres` superuser (admin))
      userPasswordKey: hive-password # Set up POSTGRES_PASSWORD env var (password for the created user)
      

# Variables related to the ACR where we keep Docker images which will be deployed in pods
acrSecret:
	secretName: acr-secret
```
### Helpers
templates/helpers.tpl:
```yaml
{{- define "hive-metastore.fullname" -}}
{{ .Release.Name }}-hive-metastore
{{- end -}}
```
### ConfigMaps with configuration files
In pods running the Thrift Server and Hive Metastore, in the `/opt/spark/conf` folder we need to have configuration files:
- `hive-site.xml`

For the Thrift Server, we need additionally in the same folder:
- `spark-defaults.conf`

We create those config files using a ConfigMap and we will mount them into the pods running the Thrift Server and Hive Metastore.

spark-configuration-configmap.yaml:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: spark-conf
data:
  hive-site.xml: |
    <configuration>

      <property>
        <name>javax.jdo.option.ConnectionURL</name>
        <value>
          jdbc:postgresql://{{ .Release.Name }}-postgresql:5432/{{ .Values.hive.database.name }}
        </value>
      </property>

      <property>
        <name>javax.jdo.option.ConnectionDriverName</name>
        <value>org.postgresql.Driver</value>
      </property>

      <property>
        <name>javax.jdo.option.ConnectionUserName</name>
        <value>{{ .Values.hive.database.user }}</value>
      </property>

      <property>
        <name>javax.jdo.option.ConnectionPassword</name>
        <value>${DB_PASSWORD}</value>
      </property>

      <property>
        <name>hive.metastore.uris</name>
        <value>
          thrift://{{ include "hive-metastore.fullname" . }}:{{ .Values.hive.metastorePort }}
        </value>
      </property>

      <property>
        <name>datanucleus.autoCreateSchema</name>
        <value>true</value>
      </property>

      <property>
        <name>hive.metastore.schema.verification</name>
        <value>false</value>
      </property>

    </configuration>
    
spark-defaults.conf: |
	# Use Hive Metastore (not the in-memory catalog)
	spark.sql.catalogImplementation=hive
	
	# Set where managed table data is stored (below is an Azure Storage Account URL)
	spark.sql.warehouse.dir=wasb://{{ .Values.spark.containerName }}@${{ .Values.spark.storageAccountName }}.blob.core.windows.net
	
	# Configs for authentication to Azure Storage Account (to be able to read and save data)
	spark.hadoop.fs.azure.account.auth.type.${MY_ACCOUNT}.dfs.core.windows.net=OAuth
	
	spark.hadoop.fs.azure.account.oauth.provider.type.${MY_ACCOUNT}.dfs.core.windows.net=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider
	
	spark.hadoop.fs.azure.account.oauth2.client.id.${MY_ACCOUNT}.dfs.core.windows.net=${CLIENT_ID}
	
	spark.hadoop.fs.azure.account.oauth2.client.secret.${MY_ACCOUNT}.dfs.core.windows.net=${CLIENT_SECRET}
	
	spark.hadoop.fs.azure.account.oauth2.client.endpoint.${MY_ACCOUNT}.dfs.core.windows.net=https://login.microsoftonline.com/${TENANT_ID}/oauth2/token
```

  where:
	- Every value `${VAR_NAME}` will be replaced with the value of the environment variable `VAR_NAME` which we will set up in pods where that ConfigMap will be mounted (it will be done by Spark / Hive inside the image, not Kubernetes)
	- `${CLIENT_ID}` and `${CLIENT_SECRET}` refers to credentials of a Service Principal with permissions for that Storage Account
	- `${MY_ACCOUNT}` is a name of our Storage Account
	- `${TENANT_ID}` - Our tenant ID from Azure
### Create a ServiceAccount + RBAC
Spark on K8s needs permissions to create executor pods.

service-account.yaml:
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: spark-thrift-sa
  namespace: spark
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: spark-thrift-rolebinding
subjects:
- kind: ServiceAccount
  name: spark-thrift-sa
  namespace: spark
roleRef:
  kind: ClusterRole
  name: edit
  apiGroup: rbac.authorization.k8s.io
```
### Thrift Server deployment
Spark provides the `start-thriftserver.sh` script. We need to run it with proper Kubernetes configs. We need to use here the `client` mode.

deployment-thrift-server.yaml:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: spark-thrift-server
  namespace: spark
spec:
  replicas: 1
  selector:
    matchLabels:
      app: spark-thrift-server
  template:
    metadata:
      labels:
        app: spark-thrift-server
    spec:
      serviceAccountName: spark-thrift-sa
      # Get a secret with credentials for authentication to the ACR.
      imagePullSecrets:
        - name: {{ .Values.acrSecret.secretName }}
      containers:
	  - name: thrift
		image: {{ .Values.spark.sparkImageUrl }}
		command:
		- /bin/bash
		- -c
		- |
		  /opt/spark/sbin/start-thriftserver.sh \
			--master k8s://https://$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT \
			--deploy-mode client \
			--name spark-thrift-server \
			--conf spark.kubernetes.namespace=spark \
			--conf spark.kubernetes.authenticate.driver.serviceAccountName=spark-thrift-sa \
			--conf spark.kubernetes.container.image={{ .Values.spark.sparkImageUrl }} \
			--conf spark.executor.instances=4 \
			--conf spark.executor.memory=4g \
			--conf spark.executor.cores=2 \
			--conf spark.sql.shuffle.partitions=200
		env:
			# Variables with:
			#   - Servie Principal's client ID and secret
			#   - Azure Tenant ID
			#   - Name of the Storage Account
			# which will be used in the spark-defaults.conf file
			- name: CLIENT_ID
			  valueFrom:
				secretKeyRef:
				  name: adls-sp-secret
				  key: client-id
			- name: CLIENT_SECRET
			  valueFrom:
				secretKeyRef:
				  name: adls-sp-secret
				  key: client-secret
			- name: TENANT_ID
			  valueFrom:
				secretKeyRef:
				  name: adls-sp-secret
				  key: tenant-id
			- name: MY_ACCOUNT
			  value: {{ .Values.spark.storageAccountName }}
		# Mount config files created in the ConfigMap
		volumeMounts:
		- name: spark-conf
		  mountPath: /opt/spark/conf
        ports:
        - containerPort: 10000
	volumes:
	- name: spark-conf
	  configMap:
		name: spark-conf
```
### Hive Metastore deployment
deployment-hive-metastore.yaml:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "hive-metastore.fullname" . }}
spec:
  replicas: 1
  selector:
    matchLabels:
      app: {{ include "hive-metastore.fullname" . }}
  template:
    metadata:
      labels:
        app: {{ include "hive-metastore.fullname" . }}
    spec:
      # Get a secret with credentials for authentication to the ACR.
      imagePullSecrets:
        - name: {{ .Values.acrSecret.secretName }}
      containers:
        - name: hive-metastore
          image: "{{ .Values.hive.image.repository }}:{{ .Values.hive.image.tag }}"
          imagePullPolicy: {{ .Values.hive.image.pullPolicy }}
          command: ["hive"]
          args: ["--service", "metastore"]
          ports:
            - containerPort: {{ .Values.hive.metastorePort }}
          env:
	        # Password to the PostgreSQL metadata db from the secret
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: hive-metastore-db-secret
                  key: hive-password
          # Mount the hive-site.xml created in the ConfigMap
          volumeMounts:
            - name: spark-conf
              mountPath: /opt/hive/conf
      volumes:
        - name: spark-conf
          configMap:
            name: spark-conf
```
### Hive Metastore service
Service for exposing Hive Metastore.

service-hive-metastore.yaml:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ include "hive-metastore.fullname" . }}
spec:
  selector:
    app: {{ include "hive-metastore.fullname" . }}
  ports:
    - port: {{ .Values.hive.metastorePort }}
      targetPort: {{ .Values.hive.metastorePort }}
```
### Thrift Server service
Service for exposing the Thrift Server.

service-thrift-server.yaml:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: spark-thrift
  namespace: spark
spec:
  selector:
    app: spark-thrift-server
  ports:
  - name: thrift
    port: 10000
    targetPort: 10000
  type: ClusterIP
```
For external access use `LoadBalancer` or `Ingress`.
# Installation
We install our Helm chart using command:
```bash
helm dependency update
helm install spark-thrift-server .
```
# Connect from clients
## Thrift Server
Now clients can connect to the Thrift Server using the JDBC URL:
```
jdbc:hive2://spark-thrift.spark.svc.cluster.local:10000/default
```
## Hive Metastore
After installation, Hive Metastore is available under URI:
```
thrift://{{ .Release.Name }}-hive-metastore:9083
```
So if we use this command for installing the chart:
```
helm install spark-thrift-server .
```
then Hive Metastore is available under:
```
thrift://spark-thrift-server-hive-metastore:9083
```
# Slow performance
If queries are slow, that might be caused by executors being created slowly. We can fix that with:
```
spark.dynamicAllocation.enabled=true
spark.dynamicAllocation.initialExecutors=2
```
