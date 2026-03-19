Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
When we use Kubernetes as a resource manager for Spark, then client (like PySpark) talks directly to Kubernetes API server, there is no Spark master.

Workflow looks like this:
1. The client talks to Kubernetes API and submits a Spark application.
2. Kubernetes creates a Spark driver pod.
3. The driver pod acts as the coordinator for the job.
4. The driver then talks to Kubernetes API to create executor pods.