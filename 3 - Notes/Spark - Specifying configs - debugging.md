Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
We can specify Spark configs either in `spark-defaults.conf` file or pass them when using the `spark-submit` command:
```
spark-submit \
	--conf conf.name=conf.value
```

Passing configs in the `spark-submit` command might help with identifying when config doesn't work properly. We can see then errors which otherwise could be hidden.