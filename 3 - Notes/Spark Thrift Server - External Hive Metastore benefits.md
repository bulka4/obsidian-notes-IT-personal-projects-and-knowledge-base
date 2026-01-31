Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Spark]]
#DataEngineering #DistributedComputing #Spark

# Introduction
By default, Thrift Server runs Hive Metastore but:
- It will be restarted if we restart the Thrift Server
- It can't be shared with other Spark jobs
- Scale to 2 replicas → corrupted metastore
- BI tools → inconsistent schema

That's it is better to deploy it as a separate service.
# Questions
- What are those problems about?
	- Scale to 2 replicas → corrupted metastore
	- BI tools → inconsistent schema
- 