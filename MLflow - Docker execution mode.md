Tags: [[__Machine_Learning_Engineering]] [[_MLflow]]
#MLEngineering #MLflow 

# Introduction
We can run a MLflow project's entrypoint ([[MLflow - Projects - Entrypoint|link]]) in a Docker mode. In that mode, MLflow will run a new Docker container and run an entrypoint in it.

To do this, we need to provide a Dockerfile or Docker image in the MLflow project like described here - [[MLflow - Projects - Environment preparation with Docker]].