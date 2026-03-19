Tags: [[_Spark]] [[__Data_Engineering]] [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
Using the `--master` and `--deploy-mode` parameters in the `spark-submit` command ([[Spark - Spark submit CLI tool|link]]), we specify in which mode to run Spark.

To run it in a local mode, we run:
```bash
spark-submit --master local[*] my_script.py
```

To run it in a cluster mode, we need to specify what resource manager to use:
```bash
# Standalone Spark
spark-submit --master spark://\<master-ip>:7077 my_script.py
# YARN
spark-submit --master yarn my_script.py
# Kubernetes
spark-submit --master k8s://https://kubernetes.default.svc my_script.py
```

To run it in a client mode, we use additionally the `deploy-mode` parameter:
```bash
spark-submit --master yarn --deploy-mode client my_app.py
```