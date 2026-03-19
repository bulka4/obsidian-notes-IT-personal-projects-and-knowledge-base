Tags: [[_Spark]] [[__Data_Engineering]], [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
The `spark-submit` CLI tool is for submitting Spark jobs, i.e. running a Spark application.

It runs a specified Spark Python script:
```bash
spark-submit [params] my_script.py
```
or a Java/Scala class:
```bash
spark-submit --class com.example.MyApp my_app.jar
```
