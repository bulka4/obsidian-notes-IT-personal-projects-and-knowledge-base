Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Satisfy prerequisites
Before we start using this code we need to satisfy all the prerequisites describe in the 'Prerequisites' section further in this document.
# Creating Azure Linux VMs
In order to create VMs using Terraform we need to run the following commands:
```
terraform init # only when running Terraform for the first time in this repository
terraform plan -out main.tfplan
terraform apply main.tfplan
```

In order to destroy all the created resources in Azure we need to run the following commands:
```
terraform plan -destroy -out main.destroy.tfplan
terraform apply main.destroy.tfplan
```
# Connecting to the created VMs from our local computer through SSH
The Terraform code will generate SSH keys pair, save the private key on our local computer and add the public key to the authorized keys on the created VMs.

Then we can connect to the created VMs by using this command on our local computer:
```
ssh username@ip_address
```

Here is described how to get values needed for SSH connection:
- **ip_address** - In order to get the ip_address values for both created VMs we need to use the Terraform outputs called 'public_ip_address_vm_1' and 'public_ip_address_vm_2'. More info about those outputs in the 'Terraform outputs' section of this documentation.
- **username**- The username value is the same as the one defined in the terraform.tfvars file for the vm_username variable.

More information about how this works is further in this document in the 'SSH key generation' section.
# Starting Hadoop and Spark cluster
In order to start the Hadoop and Spark cluster we need to connect through SSH to the VM1 which acts as a master node and run the following commands:
```shell
# Run this only when starting Hadoop cluster for the first time. If we run this later on it will remove all the data from the cluster.
$HADOOP_HOME/bin/hdfs namenode -format

# Start HDFS
$HADOOP_HOME/sbin/start-dfs.sh

# Start YARN
$HADOOP_HOME/sbin/start-yarn.sh

# Start Spark
$SPARK_HOME/sbin/start-all.sh
```

In order to learn about how to connect to that VM through SSH reference to the 'Connecting to the created VMs from our local computer through SSH' section below in this documentation.
# Accessing Jupyter Notebook
Jupyter Notebook will be started on the VM1 by executing a bash script by Terraform. To access the Jupyter Notebook from Spark use the URL:
```
public_ip_address_vm_1:8888
```

Where `public_ip_address_vm_1` is the Terraform output. More information about how to get this output is in the 'Terraform outputs' section of this documentation.

We also need to provide a password when logging into Jupyter Notebook. It is specified by the Terraform variable `jupyter_notebook_password` ('admin' by default).
# Starting Spark session
Once we are in the Jupyter Notebook, there are two options for starting a Spark session:

Using Spark Standalone mode:
```
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .appName("MySparkApp") \
    .master("spark://hadoopmaster:7077") \
    .getOrCreate()
```
The `master("spark://hadoopmaster:7077")` command specifies that we want to run Spark in the Standalone mode. The `hadoopmaster` is a hostname of the master node.

Using YARN:
```
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .appName("MySparkApp") \
    .master("yarn") \
    .getOrCreate()
```
The `master("yarn")` command specifies that we want to use YARN.
## Accessing HDFS
To browse HDFS files we need to use this URL:
```
public_ip_address_vm_1:9870
```

Where public_ip_address_vm_1 is the Terraform output. More information about how to get this output is in the 'Terraform outputs' section of this documentation.