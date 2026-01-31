Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When running containers in Kubernetes, it is a good practice to make the main process ([[Linux - Processes|link]]) running in the container (which we start with an entrypoint command) a PID 1 (to have ID = 1).

That's because, when Kubernetes wants to send a signal to a process in a container, for example to stop it, it talks to the PID 1 process and that process might not forward the signal to its child processes.

For example, if our entrypoint command looks like that:
```yaml
command: ["/bin/sh", "-c"]
args:
  - |
	export DB_URI="XXX"
	mlflow server
```

then `/bin/sh` becomes the PID 1 and `mlflow server` becomes its child. Kubernetes might try to stop the `/bin/sh` process but that stop signal will not be forwarded to the `mlflow server` process and it will be still running.

To make our main process `mlflow server` the PID 1, we can use the `exec` command:
```yaml
command: ["/bin/sh", "-c"]
args:
  - |
	export DB_URI="XXX"
	# make the `mlflow server` process the PID 1
	exec mlflow server
```