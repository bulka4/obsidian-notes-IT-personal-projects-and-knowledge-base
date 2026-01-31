Tags: [[_My_projects]]
#MyProjects 

# Run an image for interacting with AKS
Run an image for interacting with AKS using the `interacting.aks.Dockerfile` Dockerfile, connect to it and from that image perform all the next steps.
# Build and push images to ACR
Build and push to ACR all the images using the `/root/apps/build_and_push.sh` script.
# Create ACR secret
- Create a secret in every namespace with credentials for accessing Docker images in ACR
	- It stores credentials of a Service Principal with permissions to that ACR
	- We can get those values from Terraform outputs
```bash
for ns in "airflow" "spark" "mlflow"; do
	kubectl create secret docker-registry acr-secret \
		--namespace $ns \
		--docker-server=${acr_url} \ # ACR URL (<registry-name>.azurecr.io) 
		--docker-username=${client_id} \
		--docker-password=${client_secret} \
		--docker-email=unused@example.com # It doesn't matter what we put here but it is needed
done
```
# Airflow setup
- Create a secret for Storage Account
	- It stores credentials of a Service Principal used for authentication when accessing Azure Storage Account where logs will be saved
	- Values we need to provide here can be taken from Terraform outputs
```bash
kubectl create secret generic airflow-azure-blob \
  --from-literal=client_id=<client-id> \
  --from-literal=client_secret=<client-secret> \
  --from-literal=tenant_id=<tenant-id> \
  --from-literal=account_name=<storage-account-name> \
  -n airflow
```
- Install Airflow:
```bash
kubectl create namespace airflow

helm dependency update

helm install airflow ./helm_charts/airflow \
  -n airflow \
  -f values.yaml
```
# Spark Thrift Server and Hive Metastore setup
- Create a secret with Service Principal's credentials which will be used by Spark to get access to data in the Storage Account.
	  - We can get those values from the Terraform outputs
```bash
kubectl create secret generic adls-sp-secret \
  --from-literal=client-id=XXXX \
  --from-literal=client-secret=XXXX \
  --from-literal=tenant-id=XXXX \
  -n spark
```
- Create a secret for Hive Metastore for accessing PostgreSQL metadata db:
```bash
kubectl create secret generic hive-metastore-db-secret \
  --from-literal=hive-password=hivepassword \
  --from-literal=postgres-password=adminpassword \
  -n spark
```
- Install Helm chart:
```bash
helm dependency update
helm install spark-thrift-server ./helm_charts/spark_thrift_server
```
# MLflow setup
- Create a secret with credentials to the MySQL backend store. That secret will be used when installing the 'MLflow setup' Helm chart:
```bash
kubectl create secret generic mlflow-mysql \
  --from-literal=root_password=mlflow \
  --from-literal=user_password=mlflow \
  -n mlflow
```
- Create a secret with an access key to a Storage Account:
```bash
kubectl create secret generic mlflow-sa \
  --from-literal=access_key=XXX\
  -n mlflow
```
- Install Helm chart:
```bash
helm dependency update
helm install mlflow ./helm_charts/mlflow_setup
```
