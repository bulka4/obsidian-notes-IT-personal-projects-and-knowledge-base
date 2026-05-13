Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Installing Spark Operator and preparing `SparkApplication` manifest
Bash script `vm1_configure.tftpl`, which is executed by Terraform ([[Spark Operator on Kubernetes on Linux VMs project - VMs configuration|link]]):
- Creates a `SparkApplication` YAML manifest which will be used for submitting our Spark jobs. 
	- We specify there which script we want to run.
- Installs Spark Operator using Helm
- Saves a Docker image ([[Spark Operator on Kubernetes on Linux VMs project - Docker image for Spark and Jupyter Notebook|link]]) in ACR that will be used by Spark Operator to run a Spark application in pods
# Mounting a volume with Spark code
If we want to use Spark Operator to run a Spark code which was developed in Jupyter Notebook, we can do it like described here - [[Spark Operator on Kubernetes on Linux VMs project - Developing and deploying code workflow|link]], i.e. by mounting the same volume to:
- The container running Jupyter Notebook 
- Pods created by Spark Operator which runs this code.
## `SparkApplication`manifest - Mounting details
In the `SparkApplication` YAML manifest, in the `spec.mainApplicationFile` field, we specify what script we want to run:
- That is a path in the Spark Driver and Executors Pod's containers
- That path is mounted to a volume which is linked to the path on a host.

For example if we have a `SparkApplication` `YAML` manifest like that:
```
spec:
	# Spark script to run. That is a path inside the Spark Driver Pods' container.
    mainApplicationFile: "local:///opt/spark/scripts/my_script.py" 
volumes:
  - name: scripts-volume
    hostPath:
	  # path on the Kubernetes node (on the host, the VM) with Spark scripts.
      path: /home/${username}/notebooks   
      type: Directory
driver:
    volumeMounts:
     - name: scripts-volume
	   # path inside the Spark Driver Pod's container with Spark scripts.
       mountPath: /opt/spark/scripts  
executor:
    volumeMounts:
     - name: scripts-volume
       mountPath: /opt/spark/scripts
```

That means that the `/home/${username}/notebooks` path on a node (host VM), which is running Driver or Executor Pods, is linked to a volume called scripts-volume and that volume is linked to the `/opt/spark/scripts` path in the Driver and Executors Pods' containers.

So all the files from the `/home/${username}/notebooks` folder on a node, which is running Driver or Executor Pods, will be available in the `/opt/spark/scripts` folder in the Driver and Executors Pods' containers.

So the above example will run the `/home/${username}/notebooks/my_script.py` file from the node (host VM), which is running Driver or Executor Pods.
# Service account to use
Spark Operator and Spark Driver Pod need a Service Account with proper permissions for authentication for managing Pods. 

Spark Operator will have already assigned a Service Account with proper permissions after installing it with Helm. 

For Spark Driver we are creating a new Service Account in the `vm1_configure.tftpl` bash script executed by Terraform ([[Spark Operator on Kubernetes on Linux VMs project - VMs configuration|link]]).