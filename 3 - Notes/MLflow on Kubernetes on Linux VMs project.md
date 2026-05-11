Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In this project, we:
- Set up Kubernetes on Azure Linux VMs
- Run MLflow Tracking Server and project on it
- Prepare all the cloud resources needed using Terraform

This code is not production ready but is rather for learning about how to set up a multinode Kubernetes cluster and run MLflow on it.
# Code repository
Repository with the code - [github.com](https://github.com/bulka4/mlflow_kubernetes_linux_vms).
# Repository guide
Guide describing how to use this code - [[MLflow on Kubernetes on Linux VMs project - Repository guide]].
# Prerequisites
Before we start using this code we need to satisfy prerequisites - [[MLflow on Kubernetes on Linux VMs project - Prerequisites]].
# VMs and cloud resources setup
- Terraform resources creation - [[MLflow on Kubernetes on Linux VMs project - Terraform resources creation|link]] 
- Generating SSH keys for connecting to VMs - [[MLflow on Kubernetes on Linux VMs project - Generating SSH keys|link]] 
- Configuring VMs by running bash scripts on them - [[MLflow on Kubernetes on Linux VMs project - Configuring VMs using bash scripts|link]] 
# MLflow Tracking Server deployment
- Tracking Server architecture - [[MLflow on Kubernetes on Linux VMs project - Tracking Server architecture|link]] 
- Deploying the Tracking Server - [[MLflow on Kubernetes on Linux VMs project - Deploying the MLflow Tracking Server|link]] 
# Running MLflow project
[[MLflow on Kubernetes on Linux VMs project - Running MLflow project]]
# Problems and ideas for improvements
[[MLflow on Kubernetes on Linux VMs project - Problems and ideas for improvements]].