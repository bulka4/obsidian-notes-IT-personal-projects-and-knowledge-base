Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
In order to develop Spark code we can run Spark in a Local mode (on a single machine) and Jupyter Notebook (or JupyterLab or JupyterHub) in a Docker container running on a Linux VM in cloud.

Then we can connect to the Jupyter through a browser from our local computer to develop and run a Spark code.

Additionally we can use VS code with the following extensions:

· Remote-SSH - In order to connect VS code to that VM

· Dev Containers – In order to access a filesystem inside of the Docker container running on the VM.

This will give us a possibility to browse a filesystem inside of the Docker container and use terminal through VS code.

It is used in the spark_kubernetes repository.

#DataEngineering #DistributedComputing 