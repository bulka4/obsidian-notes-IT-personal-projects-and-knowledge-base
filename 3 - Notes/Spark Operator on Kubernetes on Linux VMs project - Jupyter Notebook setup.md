Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
On one of the VMs, we run Jupyter Notebook:
- We can connect to it remotely through a browser (from any machine)
- It runs in a Docker container (outside Kubernetes):
	- It is started by Terraform by executing a bash script (as described here - [[Spark Operator on Kubernetes on Linux VMs project - VMs configuration|link]])
	- It uses Docker image described here [[Spark Operator on Kubernetes on Linux VMs project - Docker image for Spark and Jupyter Notebook|link]] 
- In that container, we have prepared environment so we can run Spark code in a local mode from the Jupyter
# Mounting a volume with Spark code
We mount a folder from the host to the container running Jupyter Notebook so we can then run those scripts using Spark Operator by mounting the same volume to pods created by the Spark Operator which runs this code.

More info about it is here - [[Spark Operator on Kubernetes on Linux VMs project - Developing and deploying code workflow|link]], in the "Mounting a volume with Spark code" section.