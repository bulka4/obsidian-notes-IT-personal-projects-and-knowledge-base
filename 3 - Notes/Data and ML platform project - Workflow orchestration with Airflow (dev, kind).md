Tags: [[_My_projects]]
#MyProjects 

# Accessing Airflow webserver
We use a `nodePort` type of a Kubernetes service for the webserver. 

This service is specified in `helm_charts/airflow/values.yaml` file and we also map the port used in the `nodePort` to the host port in the kind-config file (so we can access this service from our host, not from a kind node container).

In `helm_charts/airflow/values.yaml` we specify the `NodePort` service to be used:
```yaml
webserver:
	service:
		type: NodePort
		ports:
			- port: 80          # service port (used inside the cluster)
			  targetPort: 8080  # container port
			  nodePort: 30080   # node port
```

and we map the `nodePort` to the port on the host in the kind-config file:
```yaml
nodes:
	- role: control-plane
		- containerPort: 30080
		  hostPort: 8080
		  protocol: TCP
```

Then, the traffic will go like this:
- host port (port on the host specified in the `kind-config.yaml`) ->
- container port / node port (port in the kind node container, specified in the `kind-config.yaml` as `containerPort` and in the service as `nodePort`) ->
- target port (port in the container running in the kind cluster, specified in the service)
# DAGs PV
PV (persistent volume) is used to store files with defined Airflow DAGs. It stores data on the host. 

In the `kind-config.yaml` we define where on the host data will be saved:
```yaml
nodes:
  - role: control-plane
    ...
    extraMounts:
      - hostPath: "C:/<repo-path/apps/airflow/dags"
        containerPath: /airflow_dags
```

and in `helm_charts/airflow/templates/dags-pvc.yaml` we can use `containerPath` from the kind-config as the `hostPath` parameter:
```yaml
apiVersion: v1
kind: PersistentVolume
...
spec:
  ...
  hostPath:
    path: /airflow_dags
```
# Git-sync
We use git-sync to pull code from a repo. That code will be available in pods running Airflow components (scheduler etc) and also in pods running tasks created using KubernetesExecutor and KubernetesPodOperator.

git-sync runs in a separate pod, pulls code from repo and saves it in a persistent volume. Then we can mount that volume to other pods to make the code available.

More details about how git-sync works can be found here - [[Git-sync - Kubernetes deployment]].
## Disabling git-sync
We can choose not deploy the git-sync (comment out its yaml manifest) and then we will have in PV available code from the host. We can change that code on host and it will be reflected in pods what is convenient for development. Run git-sync only to test if it works.
# Metadata db
We create a PostgreSQL db for Airflow metadata using Airflow Helm chart.

We do this so we don't pay for a managed service but for production it is recommended to use a managed service since running a database on Kubernetes is problematic as described here - [[Kubernetes - Running databases]].
# Service account
We create a service account which will be used by Airflow pods for creating new pods where tasks will be executed. 
# KubernetesPodOperator
In the Airflow dag, when using the `KubernetesPodOperator` for running a task in a new pod, we need to use `image_pull_policy="IfNotPresent"` argument so we don't try to pull an image for that pod from a remote registry but we use a local image loaded to kind instead.
# Differences from the prod deployment
This section describes how running Airflow on AKS differs from running it on kind.
## DAGs PV
In prod, as a storage for DAGs PV we use Azure File share.
## Airflow logs
In prod, Airflow logs are being saved in an Azure Storage Account.
## Service Account
In prod, Service Account uses a secret for pulling images from ACR.
## Exposing and accessing the Airflow webserver
In prod we use a load balancer service for the webserver so it gets a public IP which we use to access Airflow UI.