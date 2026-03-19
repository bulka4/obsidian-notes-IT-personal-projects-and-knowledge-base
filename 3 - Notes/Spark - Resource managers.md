Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
When we run Spark in a distributed way, on a cluster with multiple nodes (servers), we need to use a resource manager like YARN ([[_YARN|link]]), Kubernetes ([[_Kubernetes|link]]) or Standalone Spark ([[Spark - Standalone resource manager|link]]).

Resource managers are responsible for creating a driver and executor processes ([[Spark - Components - Master, driver and executors|link]]) which will be executing the code and allocating resources to them (CPU, RAM).

When we start Spark, we specify what resource manager to use using the `--master` parameter.

More information about individual resource manages can be found in the documents listed in the 'Spark resource managers' in this collection of documents - [[_Spark]].

Using the `--master` parameter in the `spark-submit` command ([[Spark - Spark submit CLI tool|link]]), we specify what resource manager to use, for example:
```bash
# Standalone Spark
spark-submit --master spark://\<master-ip>:7077 my_script.py
# YARN
spark-submit --master yarn my_script.py
# Kubernetes
spark-submit --master k8s://https://kubernetes.default.svc my_script.py
```
# Spark master and resource managers
Spark master ([[Spark - Components - Master, driver and executors|link]]) is a process which is a part of a resource manager we choose. Below are examples of what process plays the role of the master in case of different resource managers:
- Spark Standalone - There is a process called literally master ([[Spark - Standalone resource manager|link]])
- YARN - ApplicationMaster ([[YARN - Components|link]])
- Kubernetes - API server and scheduler ([[Kubernetes - Master node & worker node|link]], [[Kubernetes - Components - API server|link]], [[Kubernetes - Components - Scheduler|link]])