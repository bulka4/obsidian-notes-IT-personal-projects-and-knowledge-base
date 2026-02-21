Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
In order to start the Thrift server, we can use the script:
```bash
/opt/spark/sbin/start-thriftserver.sh \
	--master k8s: ... \
	<other-parameters>
```
or start it by submitting a Spark job:
```bash
/opt/spark/bin/spark-submit \
	--class org.apache.spark.sql.hive.thriftserver.HiveThriftServer2 \
	<other-parameters>
```

Where `<other-parameters>` are parameters which we can use (the same for both options), for example when running on Kubernetes:
```bash
/opt/spark/bin/spark-submit \
  --class org.apache.spark.sql.hive.thriftserver.HiveThriftServer2 \
  --master k8s://https://$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT \
  --name spark-thrift-server \
  --conf spark.driver.bindAddress=$POD_IP \
  --conf spark.driver.host=spark-thrift-server.spark.svc.cluster.local \
  --conf spark.driver.port=7077 \
  --conf spark.blockManager.port=7078 \
  --conf spark.kubernetes.namespace=spark \
  --conf spark.kubernetes.authenticate.driver.serviceAccountName=spark-thrift-sa \
  --conf spark.kubernetes.container.image=spark-thrift-server:latest \
  --conf spark.executor.instances=1 \
  --conf spark.executor.memory=1g \
  --conf spark.executor.cores=1 \
  --conf spark.sql.shuffle.partitions=200 \
  local:///opt/spark/jars/spark-hive-thriftserver_2.12-3.5.0.jar
```
# Submitting spark job
When we use spark submit, then the Thrift Server process runs in the foreground (there is no child process being created) and we can see logs in the console.