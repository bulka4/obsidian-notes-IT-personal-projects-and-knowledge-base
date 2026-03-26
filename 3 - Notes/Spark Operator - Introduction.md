Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
Using Spark Operator, we can run Spark jobs. It works like this:
- We create a `SparkApplication` CRD
- Spark Operator notices that CRD and creates driver pod
- Driver pod then creates executor pods

When we want to run Spark in a cluster mode, thanks to the Spark Operator there is less configuration we need to do in the Spark script.