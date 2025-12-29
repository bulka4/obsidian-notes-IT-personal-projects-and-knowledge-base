Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Kubernetes]], [[_Spark]]

# Introduction
## Created resources
After deploying SparkApplication resource it creates:
- SparkApplication resource
- Spark Driver Pod
- Spark Executor Pods
## VolumeMounts
We can use volume mounts in the SparkApplication in order to access data from a volume in the Driver and Executors Pods.
## Taints and tolerations
In order to deploy sparkApplication on a master node (control plane) we need to set up proper tolerations for SparkApplication.

We can deploy SparkApplication normally on worker nodes.

We can specify tolerations for Driver and Executors Pods in the Spark Application manifest:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps2.jpg) 

Adding tolerations requires using webhook.
## imagePullSecrets
We can use the imagePullSecrets field in the Spark Application manifest in order to access secrets which contains values for authentication to container registry from which we want to pull a Docker image used in the Spark Application.

For example we can create a secret for container registry like that:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps3.jpg) 

And use it in Spark Application:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps4.jpg) 
# Pod Template File
If we can’t add some fields in the SparkApplication manifest, then we can use Pod Template File.

We create a separate YAML manifest, which is our Pod Template File, and then we specify in Spark configuration in the Spark Application that we want to use it.

**Issues:**
I don’t know how to use it, I was trying different options:

Create a Pod Template File:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps5.jpg) 

Add the content of that Pod Template File to the ConfigMap value:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps6.jpg) 

Mount Pod Template File from configMap to the driver and executor pods, and specify in spark configuration that we want to use thos Pod Template Files:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps7.jpg) 

I was also trying to patch spark operator controller deployment to mount that volume with Pod Template File to it:

![](file:///C:\Users\mbulk\AppData\Local\Temp\ksohtml9624\wps8.jpg) 

I was always getting error that the Pod Template File can’t be found.

Someone on a forum said that they have mounted Pod Template File to Spark Operator but I don’t know how.

#DataEngineering #DistributedComputing #Kubernetes #Spark 