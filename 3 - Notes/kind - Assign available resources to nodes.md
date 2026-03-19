Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
We can change resources (CPU, RAM) available for kind nodes. We can for example:
- Decrease resources for the control plane and don't run any pods on it
- Increase resources for the worker node and run all the pods on it

Running all the pods on one node has for example such a benefit, that all the pods can use PVs with the same `hostPath`, so they will use the same folder on the host for storing PV data which will be shared with many pods.

- Find names of containers running kind nodes:
  ```bash
  docker ps
  ```
	we will see something like:
	```bash
	kind-control-plane
	kind-worker
	```
- Change limits for each node:
  ```bash
  docker update --cpus="1.0" --memory="2g" ml-control-plane
  ```