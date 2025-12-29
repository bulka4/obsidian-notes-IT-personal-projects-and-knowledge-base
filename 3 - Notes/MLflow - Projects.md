Tags: [[__Machine_Learning_Engineering]]

# Introduction
This helps you **package your ML code** with all dependencies to make it reproducible and shareable.

That can include code for:
- Training models
- Preprocess data
- Run evaluations

We can specify parameters when running a project which will be used by the code (like hyperparameters).
### Entry points
An entry point consist of a command and parameters used in that command. That command executes a function related to our ML model, for example a function for:
- Training models
- Preprocess data
- Run evaluations

Entry points are defined in a MLproject file. An example of how it looks like is in the next section ‘MLproject file’.
### MLproject file
The MLproject file is a YAML file which describes:
- Project name
- Environment (conda, docker, or system)
- Entry points (commands for running scripts)
- Parameters (if any)

It can look for example like that:
![[2 - Images/MLflow/Screenshot 2.png]]
### MLflow project content
Here is a typical folder structure for a MLflow project:
![[2 - Images/MLflow/Screenshot 3.png]]
### Docker
We can use Docker for preparing an environment where scripts (entry points) from the MLflow project will be executed.

In the MLproject file we can specify either a Dockerfile or a Docker image which will be used to prepare that environment.

Docker image which we want to use in the MLflow project can be saved either on our local computer or in a remote registry.
### Deploying on Kubernetes
In order to run our MLflow project on Kubernetes we need to include a backend_config.yaml file in the MLflow project repository (in the same folder as Dockerfile) and provide the following parameters:
![[2 - Images/MLflow/Screenshot 4.png]]

- kube-context
	- Which kube context (which Kubernetes cluster) we want to use.
	- It is required only if we are working with multiple clusters.
- Service_account
	- Name of the Service Account to use.
	- It is required only if we are pulling a Docker image from a private repository and we need to authenticate.
	- That Service Account needs to have assigned a proper role allowing for reading Kubernetes Secrets
	- It will be used to read data from a Secret which is used to authenticate to a private container repository.
- Env.MLFLOW_TRACKING_URI
	- This environment variable is needed if we are not use the default local Tracking Server but instead we have it deployed somewhere else (Kubernetes, VM, Databricks)

Then we run our project using this command:
>mlflow run . -b kubernetes -P lr=0.01 -P epochs=5 --backend-config backend_config.yaml

#MLEngineering 