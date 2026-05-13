Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We deploy a remote Tracking Server which MLflow will talk to when we run a MLflow project in order to retrieve and save metadata.

The main components we need to deploy MLflow Tracking Server are:
- Azure Storage Account - Used as an artifact store
- MySQL database - Used as an backend store
- Docker image - Where we run the Tracking Server by running the `mlflow server` command
- ACR - Used for storing the Docker image that will be used