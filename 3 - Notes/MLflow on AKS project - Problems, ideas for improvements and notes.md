Tags: [[_My_projects]]
#MyProjects 

# Introduction
Sometimes when running the container for interacting with AKS, kubeconfig file is not configured properly and we are not able to use kubectl to interact with AKS.

In that case it helps to run again, in the running container, code from the Dockerfile under this comment: 'Install Azure CLI and save credentials to AKS in the ~/.kube/config (kubeconfig) file'.

I don't know what this is about as this issue appears only sometimes. Maybe it is something about Docker caching.
## Helm charts deployment issue
Sometimes when we install the 'MLflow setup' Helm chart, it doesn't deploy all the resources and we need to try to install it again.
## Running MLflow project with Kubernetes backend
Instead of running MLflow project in a local mode, we can use an option to run it with Kubernetes backend as described here [mlflow.org/docs](https://www.mlflow.org/docs/latest/ml/projects/#remote-execution).

In this case we run the `mlflow run` command from our local computer and MLflow takes care of creating Kubernetes resources.

I was not using this approach in this project as it looks like this approach requires to have Docker installed. So if we would like to run this command from inside of the container for interacting with AKS, we would need to have Docker installed in this container (which is tricky to do).

Also it looks like MLflow tries to pull an image from ACR to the host where we run `mlflow run` and we need to be logged in to Azure. I don't know why, since we are running the project on Kubernetes, so image should be pulled by Kubernetes resource.