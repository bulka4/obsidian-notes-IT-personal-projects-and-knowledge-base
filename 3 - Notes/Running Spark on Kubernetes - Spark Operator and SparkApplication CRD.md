Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Kubernetes]], [[_Spark]]

# Introduction
Here are the steps we need to follow to submit a Spark job using this method:
- Prepare a Spark script
- Build a Docker image where we can run our Spark script
- Push that Docker image to the container registry
- Create a SparkApplication CRD (YAML manifest)
- Deploy SparkApplication (which will run the Spark script) using for example kubectl or Airflow

The Spark script which we want to run needs to be either contained in the Docker image we build or mounted into it.

Instead of pushing Docker image to a container registry we can use an image saved on each Kubernetes’ node.

In the SparkApplication YAML manifest we can specify for example:
- Which Docker image we want to use
- Which Spark script to run
# Pros
- Observality
	- All the logs well structured in SparkAplication resource (no need to check multiple Pods)
	- Job status easy to see in SparkApplication
	- Easy integration with Prometheus, Grafana, Spark History Server
- Resource cleanup
	- Automatically cleans up driver and executor pods after executing a job
	- We only need to clean sparkApplication resource
- Job templating and parametrization
	- Specifying job parameters using YAML file
	- Easier to work with compared to CLI commands
- Retry support
	- It can retry a single Executor Pod.
# Cons
- Difficult to set up.
# Prerequisites

In order to use the SparkApplication YAML manifest we need to:
- Install Spark Operator using Helm
- Create a Service Account with proper permissions.

That Service Account will be used by the Spark Driver Pod to create Executors Pods.

Spark Operator will have automatically assigned a Service Account with proper permissions when using Helm.
# How this works in more detail
1. We prepare a SparkApplication YAML manifest
2. We deploy it, for example using the ‘kubectl apply’ command or using Airflow operator. That creates a SparkApplication resource.
3. Spark Operator notices that we created a SparkApplication resource and starts processing it.
4. Spark Operator creates a Spark Driver Pod.
5. Spark Driver Pod creates Spark Executor Pods.
6. Spark Pods executes Spark scripts.
7. Once the scripts are finished, Spark Pods are terminated.
