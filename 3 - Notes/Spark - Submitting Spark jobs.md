Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
We can submit Spark jobs in two primary deployment modes:
- Local mode
- Cluster mode

Depending on environment we can submit Spark jobs using different tools, for example:
- Running a Python script
- Using spark-submit or pyspark CLI tool
- Using Kubernetes Spark Operator and SparkApplication CRD.
## Local mode
When we run Spark in a local mode, that means it is running on a single machine. Then we have only one JVM (Java virtual machine) process.

In order to run Spark in a local mode, we can use one of the following commands:
- Python script.py
- spark-submit --master local[*]" my_script.py
- pyspark --master local[*]" my_script.py

Instead of specifying a master in the above commands we can do it in the script when creating a SparkSession:
- SparkSession.builder.master("local[\*]").getOrCreate()
## Cluster mode
When we run Spark in a cluster mode, that means it is running on multiple machines in a distributed way. We have then multiple JVM porcesses (master and workers) running on different machines.

Cluster mode requires to use a resource manager like YARN, Kubernetes or Standalone Spark.

How we submit Spark jobs depends on which resource manager we are using.
### Standalone Spark
In order to run Spark using the Standalone Spark resource manager (i.e run it in the Standalone mode) we need to use one of those commands:
- spark-submit --master spark://\<master-ip>:7077 my_script.py
- pyspark --master spark://\<master-ip>:7077 my_script.py

Where master-ip is a IP address of the Spark Master node.

We can specify master in the command like shown above or we can specify it in the script when creating a SparkSession:
- SparkSession.builder.master("spark://\<master-node-ip-address>:7077").getOrCreate()
### YARN
In order to submit a Spark job using YARN we use the same methods as in the Standalone Spark, that is we use either spark-submit or pyspark CLI tools. We just need to specify a different master:
- spark-submit --master yarn my_script.py

More information about running Spark with YARN can be found in the ‘Spark on YARN’ document in the same folder as this one.
### Kubernetes
In order to submit a Spark job using Kubernetes we can use the spark-submit CLI tool like in case of YARN:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml13036\wps9.jpg) 

Or we can also use the Spark Operator and SparkApplication CRD.

In that case we create a YAML file where we provide parameters specifying how the Spark job will be executed.

More information about running Spark with Kubernetes can be found in the ‘Spark on Kubernetes document in the same folder as this one.

#DataEngineering #DistributedComputing 