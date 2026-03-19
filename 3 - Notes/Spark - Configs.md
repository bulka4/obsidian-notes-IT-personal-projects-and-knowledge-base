Tags: [[_Spark]] [[__Data_Engineering]] [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
Before we run a Spark app, we need to prepare configs. There are 3 different places where we can put those configs:
- In the `$SPARK_HOME/spark-defaults.conf` file (`SPARK_HOME` is usually `/opt/spark`)
- If using `spark-submit` command ([[Spark - Spark submit CLI tool|link]]), then we can pass configs in that command:
  ```bash
	spark-submit script.py \
	  --master ... \
	  --conf config_name_1=value_1 \
	  --conf config_name_2=value_2 \
	  ...
  ```
- In the Python code with the Spark app we run, when creating a SparkSession ([[SparkSession|link]]):
  ```python
	spark = SparkSession.builder \
    .appName("write_iceberg") \
    .master("k8s://https://kubernetes.default.svc") \
    .config("config_name_1", value_1) \
    .config("config_name_2", value_2) \
    ...
  ```
  or:
  ```python
	import os

	conf = {
	    config_1: value_1
	    ,config_2: value_2
	}
	
	builder = SparkSession.builder \
		.appName("write_iceberg") \
		.master("k8s://https://kubernetes.default.svc") \
	for k, v in conf.items():
	    builder = builder.config(k, v)
	
	spark = builder.getOrCreate()
  ```
  