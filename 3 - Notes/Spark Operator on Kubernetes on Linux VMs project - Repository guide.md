Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Satisfy prerequisites
Before we start using this code we need to satisfy all the prerequisites described here - [[Spark Operator on Kubernetes on Linux VMs project - Prerequisites]].
# Creating Azure Linux VMs
Create and configure VMs using Terraform we need to run the following commands:
- It might take around 10 - 15 minutes (executing bash scripts on VMs takes time)
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
For next steps, we will need to connect to created VMs using SSH.

The Terraform code will generate SSH keys pair ([[Spark Operator on Kubernetes on Linux VMs project - Generating SSH keys|link]]) which we can use to connect to the created VMs by using this command on our local computer:
```
ssh username@ip_address
```

Here is described how to get values needed for SSH connection:
- **ip_address** - In order to get IP addresses of both created VMs we need to use the Terraform outputs (more info here - [[Spark Operator on Kubernetes on Linux VMs project - Terraform outputs|link]]) called `public_ip_address_vm_1` and `public_ip_address_vm_2`
- **username**- The username value is the same as the one defined in the `terraform.tfvars` file for the `vm_username` variable (or the default one "azureadmin" defined in the `variables.tf`).
# Setting up a Kubernetes cluster
When we run `terraform apply`, Terraform performs the initial setup of Kubernetes ([[Spark Operator on Kubernetes on Linux VMs project - Terraform - VMs setup|link]]) but the worker node is not added to the cluster yet, we need to add it manually by following the steps:
- Connect from our local computer to the VM1 using SSH
- Copy the join command using the `cat /home/azureadmin/k8s_join_workers.txt` command
- Connect to VM2 using SSH
- Run the copied command on the VM2 using `sudo`: `sudo <copied-command>` 
## Verify that the cluster is running
In order to confirm that the cluster is running we can do the following things:
- Run the `kubectl get pods -n kube-system` command
	- It lists required system Pods
	- All the listed Pods there should have status 'Running'
	- Pods might have status 'In progress' at the beginning and change it into 'Running' after some time
- Run the `kubectl get nodes` command
	- It should list two nodes 'master' and 'worker1' with the 'Ready' status. 
	- Again it might take some time before they get from the 'In progress' into 'Ready' status.
	- Before both nodes get status 'Ready', the previous command must show that all the system Pods are Running.
# Accessing Jupyter Notebook
To access the Jupyter Notebook use the URL:
```
public_ip_address_vm_1:8888
```

Where `public_ip_address_vm_1` is the Terraform output (how to get an output - [[Spark Operator on Kubernetes on Linux VMs project - Terraform outputs|link]]).

Password to the Jupyter Notebook is specified by the Terraform variable `jupyter_notebook_password` ('admin' by default).
# Starting Spark session
This section describes how to set up Spark session within a PySpark script.
## Local mode
Once we are in the Jupyter Notebook, we can create a Spark session in the following way:
```python
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .appName("SparkTest") \
    .master("local[*]") \
    .getOrCreate()
```

Where `master("local[*]")` indicates that we want to run Spark in a local mode.
## Cluster mode
If we want to run the Spark script in a cluster mode on Kubernetes using Spark Operator, then we need to create Spark session like that:
```Python
from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .appName("SparkTest") \
    .getOrCreate()
```

We don't specify here the master. It will be added automatically by the Kubernetes Spark Operator.
# Running Spark script on Kubernetes using Spark Operator
We can either use the prepared testing script saved at `/home/azureadmin/notebooks/my_script.py` at both VMs or we can create our own script through Jupyter Notebook.

In order to run a Spark script on Kubernetes we need to deploy a `SparkApplication` resource using prepared manifest:
```
kubectl apply -f ~/k8s/spark_application.yaml
```
## Path to the script to run
In the `~/k8s/spark_application.yaml` manifest, in the `spec.mainApplicationFile` field is specified a path to the script which we want to run. 

That is a path inside a Spark Driver Pod's container to which we mount a volume linked to a folder on a host.

More information about how this works is in other sections of this documentation:
- 'SparkApplication volumes and volumeMounts'
- 'Workflow - developing code in Jupyter and deploying on Kubernetes'
- 'Docker image for Spark and Jupyter Notebook' (especially the 'Docker image - Bind mounting' subsection)