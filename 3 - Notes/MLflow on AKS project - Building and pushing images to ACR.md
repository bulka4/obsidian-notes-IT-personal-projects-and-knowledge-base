Tags: [[__My_projects]]
#MyProjects 

# Introduction
When starting a container for interacting with AKS, the `build_and_push.sh` bash script will be executed which will build and push to ACR Docker images.

This script is using files from the docker > mlflow_docker folder (which is copied from the repo into the image). In this folder we have Dockerfiles for building images and other files used by those Dockerfiles.

We build two images:
- **Image for running MLflow project**
    - It contains Python installed and all the libraries used in the project
    - For building it we use the mlproject.Dockerfile and mlproject_requirementx.txt files
    - The mlproject_requirementx.txt contains Python libraries needed to run the project
- **Image for deploying MLflow Tracking Server**
    - For that we use the tracking-server.Dockerfile file
    - It has installed packages needed to run the Tracking Server which uses Azure Storage Account as an artifact store and MySQL as a backend store.