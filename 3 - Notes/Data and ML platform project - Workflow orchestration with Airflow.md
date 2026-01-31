Tags: [[_My_projects]]
#MyProjects 

# Kubernetes deployment
How to deploy Airflow on Kubernetes is described here - [[Airflow - Kubernetes deployment]].
# Helm chart
To deploy Airflow on Kubernetes we use the official Helm chart. It is used as a dependency in the `helm_charts/airflow/Chart.yaml` file and in the same folder Terraform will create the `values.yaml` file.
## values.yaml
The `values.yaml` file will be provided for that chart in the `helm_charts/airflow` folder and it will be created by Terraform.

It interpolates the `terraform/template_files/helm_charts/values-airflow.yaml` template to create it ((inserts variables values into the template file). 
# Git-sync
We use git-sync to pull code from the repo, with Airflow tasks to run, create a volume and mount it into pods created by Airflow where that code runs.

We create a separate PVC which will be used by git-sync to store code there, so we can later use this PVC to mount it to other pods, for example pods created by Airflow for executing tasks using KubernetesPodOperator.

By default, git-sync would create a volume available only for Airflow pods (scheduler etc).
# Airflow logs
Airflow logs are being saved in Azure Storage Account. We configure that in the `values.yaml` file.
## Service Principal
We create a connection which uses credentials of a Service Principal with permissions to connect to Storage Account (it is configured also in the `values.yaml` file)
# Metadata db
We create a PostgreSQL db for Airflow metadata using Airflow Helm chart.

We do this so we don't pay for a managed service but for production it is recommended to use a managed service since running a database on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].