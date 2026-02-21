Tags: [[__Data_Engineering]], [[__Distributed_computing]]
#DataEngineering #DistributedComputing 

# Introduction
If we try use the `/opt/spark/sbin/start-thriftserver.sh` script in order to start the Thrift server in a Kubernetes pod, then pod will get the `completed` status.

That's because the Thrift Server process started by the script is running in the background, not as a PID 1 process.

In order to avoid this, we can try one of the below solutions.
# Use spark-submit
We can start the Thrift Server by submitting a Spark job like described here - [[Spark Thrift Server - Starting the Thrift Server|link]]. This is the recommended way.

Parameters to use:
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
where:
- class - What class to run
- master - Which cluster manager to use (YARN, Kubernetes etc)
- spark.driver.bindAddress - An IP address to which Spark Driver will bind (it will listen on that IP). That should be IP of the Kubernetes pod where Thrift Server and Spark Driver are running. We can get pod's IP by creating an env var like this:
```yaml
- name: POD_IP
  valueFrom:
	fieldRef:
	  fieldPath: status.podIP
```
- spark.driver.host - DNS name of the server running the Spark driver
- spark.driver.port and spark.blockManager.port - Might be needed (I am not sure) so driver can bind to a proper port (start listening on that port)
- serviceAccountName - Name of the service account with permissions for creating pods etc. It will be used by the Driver to create Spark Executor pods
- The exact name of the `spark-hive-thriftserver_2.12-3.5.0.jar` jar we can find in our `/opt/spark/jars` folder
# Run another command which runs forever
After running the `/opt/spark/sbin/start-thriftserver.sh` script in the pod's entrypoint, we can run another command which will run forever, for example:
```bash
/opt/spark/sbin/start-thriftserver.sh \
&& tail -f /dev/null
```