Tags: [[_My_projects]]
#MyProjects 

# Kubernetes deployment
How to deploy Airflow on Kubernetes is described here - [[Airflow - Kubernetes deployment]].
# Helm chart
To deploy Airflow on Kubernetes we use the official Helm chart. It is used as a dependency in the `helm_charts/airflow/Chart.yaml` file and in the same folder Terraform will create the `values.yaml` file.
## values.yaml
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
# Airflow logs
Airflow logs are being saved in Azure Storage Account. We configure that in the `values.yaml` file.
## Service Principal
We create a connection which uses credentials of a Service Principal with permissions to connect to Storage Account (it is configured also in the `values.yaml` file)
# Metadata db
We create a PostgreSQL db for Airflow metadata using Airflow Helm chart.

We do this so we don't pay for a managed service but for production it is recommended to use a managed service since running a database on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].