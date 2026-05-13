Tags: [[__My_projects]] [[__Machine_Learning_Engineering]]
#MyProjects #MLEngineering 

# Introduction
This repository contains Terraform code which:
- Creates AKS
- Generates a Dockerfile - Which can be used to run a container with prepared environment to interact with created AKS. From that container we can:
    - Deploy MLflow Tracking Server on AKS
    - Run MLflow project on AKS

For deploying MLflow Tracking Server and running MLflow project we will be using Helm charts from this repository, in the docker > helm_charts folder:
- mlflow_project - Running a project
- mlflow_setup - Deploying Tracking Server and preparing other resources needed to run the project

Both Helm charts will be copied to the container for interacting with AKS.
# Repository guide
Read this first before start working with code from this repo:
1. [[MLflow on AKS project - Important notes before you use this repo]]
2. [[MLflow on AKS project - Repository guide]]
3. [[MLflow on AKS project - Prerequisites]]
# Infrastructure setup
1. [[MLflow on AKS project - Docker container for interacting with AKS]]
2. [[MLflow on AKS project - Creating Azure resources with Terraform]]
# Helm chart
Helm chart for deploying the MLflow Tracking Server and preparing resources needed to run MLflow projects:
1. [[MLflow on AKS project - MLflow setup Helm chart]]
# Running MLflow projects
How to prepare a MLflow project for training and evaluating model:
1. [[MLflow on AKS project - MLflow project]]
# Problems and ideas for improvements
1. [[MLflow on AKS project - Problems and ideas for improvements]]