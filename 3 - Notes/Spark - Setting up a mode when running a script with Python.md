Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
When we run a Spark script using Python ([[Spark - Clients starting calculations|link]]):
```bash
python spark_script.py
```
and in the script we create a session, then we can run Spark either in the local mode or in the client mode.

To run it in the local mode, we create a session like this:
```python
spark = SparkSession.builder \
    .appName("app_name") \
    .master("local[*]") \
    .getOrCreate()
```

And to run it in the client mode, we create a session like this:
```python
spark = SparkSession.builder \
    .appName("app_name") \
    .master("yarn") \ # or other resource manager
    .getOrCreate()
```
we need to choose here some resource manager ([[Spark - Resource managers|link]]) to use, like YARN, Kubernetes or Spark Standalone.

We can't run Spark in the cluster mode when running Spark script using Python.