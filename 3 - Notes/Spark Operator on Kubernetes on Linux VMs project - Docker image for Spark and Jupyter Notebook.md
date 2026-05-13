Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
We create a Docker image that can be used to:
- Run Jupyter Notebook ([[Spark Operator on Kubernetes on Linux VMs project - Jupyter Notebook setup|link]])
- Run Spark in a local mode (e.g. from Jupyter Notebook, for code development)
- Run Spark jobs ([[Spark Operator on Kubernetes on Linux VMs project - Running Spark jobs with Spark Operator|link]]) in a cluster mode on Kubernetes using Spark Operator ([[Spark Operator on Kubernetes on Linux VMs project - Preparing Spark Operator and `SparkApplication` CRD|link]])

We can use this image for both Jupyter and Spark Operator because we can choose whether or not to launch a Jupyter Notebook when starting a container.
# Preparing the Dockerfile and saving image in ACR
Terraform runs a bash script on a VM ([[Spark Operator on Kubernetes on Linux VMs project - VMs configuration|link]]) which:
- Creates a Dockerfile for creating this image
- Saves the image in ACR (so it can be used by Spark Operator to run Spark jobs) 
# Docker image - Deciding whether or not to launch a Jupyter Notebook
We can choose whether or not to launch a Jupyter Notebook when running a container:
- We do this by setting up a value of the `LAUNCH_JUPYTER` environment variable (true or false, it is used in the `entrypoint.sh` script)
- We don't launch Jupyter Notebook when we want to use this image to run Spark job using Spark Operator (then we just run the Spark script)