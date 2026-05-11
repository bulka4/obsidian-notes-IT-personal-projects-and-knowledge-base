Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In this project, we:
- Set up Kubernetes on Azure Linux VMs
- Set up Jupyter Notebook on one VM for code development (where we can run Spark in a local mode)
- Create all the cloud resources needed using Terraform
- Enable running Spark scripts developed in Jupyter Notebook in a cluster mode on Kubernetes using Spark Operator

This code is not production ready but it is a good starting point for preparing a framework for submitting Spark jobs on Kubernetes using Spark Operator. 

It helps with learning how to:
- Configure a multi node Kubernetes cluster
- Submit Spark jobs using Spark Operator
# Code repository
Repository with the code: [github.com](https://github.com/bulka4/spark_kubernetes_linux_vms).
# Repository guide
guide describing how to use this code - [[Spark Operator on Kubernetes on Linux VMs project - Repository guide]].
# Prerequisites
Before we start using code from this project, we need to satisfy prerequisites described here - [[Spark Operator on Kubernetes on Linux VMs project - Prerequisites]].
# Infrastructure setup
- Creating Azure resources with Terraform - [[Spark Operator on Kubernetes on Linux VMs project - Creating Azure resources with Terraform|link]] 
- Generating SSH keys to connect to created VMs - [[Spark Operator on Kubernetes on Linux VMs project - Generating SSH keys|link]] 
- VMs configuration - [[Spark Operator on Kubernetes on Linux VMs project - VMs configuration|link]] 
- Kubernetes cluster setup - [[Spark Operator on Kubernetes on Linux VMs project - Kubernetes cluster setup|link]] 
- Jupyter Notebook setup for code development - [[Spark Operator on Kubernetes on Linux VMs project - Jupyter Notebook setup|link]] 
- Docker image for Spark and Jupyter Notebook - [[Spark Operator on Kubernetes on Linux VMs project - Docker image for Spark and Jupyter Notebook|link]] 
- Preparing Spark Operator and `SparkApplication` CRD - [[Spark Operator on Kubernetes on Linux VMs project - Preparing Spark Operator and `SparkApplication` CRD|link]] 
# Development workflow
How to develop and run Spark code on this Kubernetes platform:
- Developing and deploying code workflow - [[Spark Operator on Kubernetes on Linux VMs project - Developing and deploying code workflow|link]] 
- Running Spark jobs with Spark Operator - [[Spark Operator on Kubernetes on Linux VMs project - Running Spark jobs with Spark Operator|link]] 
# Problems and ideas for improvements
[[Spark Operator on Kubernetes on Linux VMs project - Problems and ideas for improvements]]
