Tags: [[_My_projects]]
#MyProjects 

# Introduction
For data transformation we use dbt and Spark. It is better to use Thrift Server rather than Spark Operator because with the Thrift Server we have a persistent Spark session while Spark Operator creates a new session for every dbt run.

Why it is better to have a persistent session is described here - [[dbt with Spark]].
# Thrift Server
Deploying Thrift Server on Kubernetes is described here - [[Spark Thrift Server with an external Hive Metastore - Kubernetes deployment]].
# Docker image
For running Spark Thrift Server, we use the official Spark image with:
- Spark built with Hive support
- `spark-hive` JARs
- Additional tools enabling connecting Spark to Azure Storage Account

For Hive Metastore we unchanged official image.
# External Hive Metastore
We use an external Hive Metastore (running as a separate deployment) which has benefits as described here - [[Spark Thrift Server - External Hive Metastore benefits|link]].
# Data storage
We store data used for Spark calculations (including managed tables' data) in Azure Storage Account.
# PostgreSQL
PostgreSQL used as a metadata db for Hive Metastore is deployed as a dependency in this Helm chart using the official PostgreSQL Helm chart.

For production it is recommended to use a managed PostgreSQL as running databases on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
## PVC
By default, the official PostgreSQL Helm chart creates a PVC. On AKS, that PVC will use an Azure disk by default.
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
