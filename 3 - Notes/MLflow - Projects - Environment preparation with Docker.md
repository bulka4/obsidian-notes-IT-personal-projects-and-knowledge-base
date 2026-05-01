Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can use Docker for preparing an environment where entrypoints ([[MLflow - Projects - Entrypoint|link]]) from the MLflow project will be executed.

When we run an entrypoint, MLflow can run a container and run that entrypoint in that container.

In a MLproject file ([[MLflow - Projects - MLproject file|link]]) we can specify either:
- A Dockerfile
- A Docker image
	- From a localhost
	- Or from a remote registry
which will be used to run a container where an entrypoint will be executed.