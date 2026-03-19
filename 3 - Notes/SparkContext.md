Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
SparkContext is a logical object which lives inside of a Spark driver ([[Spark - Components - Master, driver and executors|link]]). We need to have a Spark driver running, and then SparkContext can be created inside of that driver.

SparkContext represents a connection between our Spark application and the Spark cluster.

It is responsible for:
- Connecting to the resource manager ([[Spark - Resource managers|link]]) (like YARN or Kubernetes)
- Requests executors and resources for them from the cluster manager
- Scheduling tasks (assigning them to executors)
- Communicating with executors
- Providing APIs for RDD operations

Example:
```python
from pyspark import SparkContext  
  
sc = SparkContext(
	master="yarn"    # Specify what resource manager to use
	appName="MyApp"
)  
  
rdd = sc.parallelize([1,2,3,4])  
print(rdd.map(lambda x: x*2).collect())
```

In Python (and other languages), we typically use SparkSession ([[SparkSession|link]]), which internally manages the SparkContext.