Tags: [[__DevOps]]

In order to develop code we can run Jupyter Notebook (or JupyterLab or JupyterHub) in a Docker container running on a Linux VM in cloud. That container will be properly set up for running code.

Then we can connect to the Jupyter through a browser from our local computer to develop and run a code.

Additionally we can use VS code with the following extensions:
- Remote-SSH - In order to connect VS code to that VM
- Dev Containers – In order to access a filesystem and shell session inside of a Docker container

We can use both those extensions together in order to first connect to a remote VM through SSH and then get access to filesystem and shell session of a container running on this remote VM.

This will give us a possibility to browse and edit files, and run code inside of the Docker container running on the remote VM.

It is used in the spark_kubernetes repository.