Tags: [[_Spark]] [[__Data_Engineering]] [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
To run Spark in the client mode ([[Spark - Modes|link]]), it is worth to be familiar with the below configs ([[Spark - Configs|link]]).

Let's remind in short, that in the client mode the Spark driver runs on the same server where we run the Spark app and it creates executor pods on any server in the cluster.

Configs:
- `spark.driver.bindAddress` - IP address to which Spark driver will bind (it will listen on that IP). That should be IP of the server where we run this script
  
  I think that if we set it up to `0.0.0.0` then it will always work (but I am not sure).
- `spark.driver.host` - DNS name of the Spark driver which will be used by executor pods to talk to the driver. 
  
  Since we run Spark in the client mode, then driver will run on the server where we run this script, so `driver.host` should be the DNS name of that server.
- `spark.driver.port=7077` and `spark.blockManager.port=7078` - might be needed (I am not sure) so driver can bind to a proper port (start listening on that port)

Additionally, if running Spark on Kubernetes:
- `spark.kubernetes.namespace` - Kubernetes namespace where to create executor pods (it should be the same as namespace where the Spark driver is, i.e. where we run the Spark app)