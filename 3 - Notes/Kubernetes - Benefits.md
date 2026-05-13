Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[_Kubernetes]]

# Introduction
This document outlines how Kubernetes can be leveraged in the data analytics domain. It includes real-world examples, benefits, and the reasons why Kubernetes is a strong fit for modern, distributed data processing workflows.
# Use cases
Generally Kubernetes is useful when we want to run multiple applications distributed across multiple servers. Using Kubernetes we can set up and manage environments (containers) in which each application is running.

For example we can run on one Kubernetes cluster the following services:
- Airflow – Workflow orchestration
- Data ingestion processes – Python scripts
- Spark - Distributed data transformation
- MiniIO - Distributed object storage
- Mlflow – Managing ML models lifecycle
- Custom automation scripts – Interacting with APIs of tools like PowerBI, Databricks or Azure.

Each component of those services can run in an isolated containerized environment, for example:
- **Airflow**
	- Webserver
	- Scheduler
	- Workers
- **Spark**
	-  Driver
	-  Executors
- **Each data ingestion process**
# Benefits
Benefits which Kubernetes offers are:
## Isolation
- Each application is running in a separate container with dedicated dependencies.
- Application dependencies do not conflict.
- Application’s failures don’t affect other applications.
## High Availability and Fault Tolerance
Easy to:
- Create multiple replicas of an application
- Replace crashed replica with another one
- Retry failed batch jobs

Make zero-downtime deployments of apps’ updates possible - immediately replace an old application with a new one once it is ready.
## Networking
- Kubernetes can assign a static IP address and DNS names to the application (a container running an app)
- Even after restart of a container, it will still have the same IP address and DNS name.
## Easy management of multiple containerized applications
We can efficiently manage multiple containerized applications by deploying them in a declarative way with YAML files.

Those configuration YAML files allow for example to define:
- How many resources that application can use (CPU, RAM)
- Environmental variables
- What bash script to execute before application starts
- What volumes to mount

This enhances reproducibility, automation and supports version control with Git.
## Container scheduling
 Automatically:
- Assign resources (CPU, RAM) to containerized applications 
- Find a server which to run it on
## Scaling
Easily add servers to a Kubernetes cluster.