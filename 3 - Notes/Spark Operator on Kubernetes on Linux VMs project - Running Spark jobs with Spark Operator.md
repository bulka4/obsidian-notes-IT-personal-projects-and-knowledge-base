Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
In order to run Spark script we need to deploy a `SparkApplication` resource. It can be deployed:
- Manually using `kubectl`
- Automatically on schedule using Airflow

In the `SparkApplication` manifest we are defining what script we want to run. Once we deploy it:
- Spark Operator notices that and creates a Spark Driver Pod
- Then, Driver Pod creates Spark Executors Pods.
# Prerequisites
In order to run Spark jobs using Spark Operator, we need to make preparations like described here - [[Spark Operator on Kubernetes on Linux VMs project - Preparing Spark Operator and `SparkApplication` CRD|link]].
# Mounting a volume with a Spark application to run
We can:
- Develop a Spark application using Jupyter Notebook
- Save the application in a volume
- Mount the volume to the pods created by Spark Operator to run the application from it

More info about it is here - [[Spark Operator on Kubernetes on Linux VMs project - Developing and deploying code workflow|link]].