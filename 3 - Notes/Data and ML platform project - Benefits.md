Tags: [[__My_projects]]
#MyProjects 

# Introduction
The main benefits of this platform.
# Data storage
Object data storage we use is:
- Distributed
- Easy to scale
- Decoupled from compute (we can easily scale separately storage and compute resources)
# Data transformations
dbt provides:
- Automatic dependency resolution (deciding in which order to build tables such that first we build dependency tables and then tables that aredependent on them)
- Tags enabling building a specific set of tables easily with a single command

Additionally, we have:
- Distributed calculations with Spark
- A lot of flexibility with Spark and Python functions
# Data ingestion
- We can run scripts in any programming language for data ingestion.
	- Python is probably the best for the most of cases because it is easy to use and flexible
- We can configure networking on AKS (Azure Kubernetes) to access external systems
	- We can create a VNet which we can connect to another network
# Data governance
Thanks to dbt we can:
- Create table and columns descriptions
- Automatically generate data lineage graphs
# Workflow orchestration
Airflow allows to schedule DAGs ([[Airflow - DAGs|link]]) which are workflows consisting of multiple tasks to execute.

It provides a lot of flexibility when it comes to:
- What tasks we can run:
	- we can run on schedule any script, in any programming language, in an environment (Kubernetes pod) which has everything needed for the script to work (libraries, tools, environment variables etc.)
- How do we schedule DAGs. We can run a DAG:
	- At a specific time (e.g. everyday at 8 am)
	- With a specific frequency (e.g. every 2h)
	- When another DAG completes
- How do we execute tasks within a DAG:
	- Wait for some event to happen before starting executing a task
	- One task starts automatically right after the previous task has been finished
	- Skip next, downstream tasks when a specific condition is not satisfied
# Container orchestration and server scaling
Thanks to Kubernetes we get:
- **Isolation** - Each application is running in a separate container with dedicated dependencies.
- **Scaling** - Easily add servers to a Kubernetes cluster
- **Container scheduling** - Automatically:
	- Assign resources (CPU, RAM) to containerized applications 
	- Find a server which to run it on
- **Networking** - Build-in DNS resolution
- **High Availability and Fault Tolerance** - Easy to:
	- Create multiple replicas of an application
	- Replace crashed replica with another one
	- Retry failed batch jobs
	
	Additionally, make zero-downtime deployments of apps’ updates possible - immediately replace an old application with a new one once it is ready.
- **Easy management of multiple containerized applications** - Efficiently, in a declarative way define how to deploy all the applications using YAML configuration files.