Tags: [[_Spark]]
#Spark 

# Introduction
SparkSession is the main tool for working with DataFrames and SQL. It allows to create DataFrames and run SQL queries.

It is a higher-level abstraction that wraps multiple contexts:
- SparkContext ([[SparkContext|link]])
- SQLContext
- HiveContext

Just like a SparkContext, it is also a logical object that lives in a Spark driver ([[Spark - Components - Master, driver and executors|link]]) and we need to have a driver running to create a session in it.

When we interact with SparkSession, it uses internally SparkContext which is responsible for (like also described here - [[SparkContext|link]]):
- Connecting to the resource manager ([[Spark - Resource managers|link]]) (like YARN or Kubernetes)
- Requests executors and resources for them from the cluster manager
- Scheduling tasks (assigning them to executors)
- Communicating with executors
- Providing APIs for RDD operations

Example:
```python
from pyspark.sql import SparkSession  
  
spark = SparkSession.builder \  
.master("k8s://https://cluster") \  # Specify what resource manager to use 
.appName("MyApp") \  
.getOrCreate()  
  
df = spark.read.csv("data.csv")  
df.groupBy("country").count().show()

result = spark.sql("SELECT country, COUNT(*) as cnt FROM people GROUP BY country")
```

Inside a session, Spark:
- loads catalog ([[Data storage catalog|link]]) metadata
- caches information
- remembers configuration
- keeps runtime statistics
- keeps temporary objects
- keeps internal optimizer behavior settings
	- That creates execution plans which determines how SQL statements are executed
# Creating a SparkSession - practical examples
More practical examples of how we can create a SparkSession are in documents below:
- 