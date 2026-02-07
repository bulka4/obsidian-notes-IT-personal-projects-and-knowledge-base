Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Volumes are a resource which works like volumes in Docker. Volumes allow us to save data from a container outside of a container (on a host running a container).

So container will be using this data and even after container restart, that data will be still accessible.

Volumes need to be used together with VolumeMounts which will specify the path in the container where data from a Volume will be accessible.

We can additionally use the hostPath parameter to specify where data from a Volume will be stored on a host.
# Volume
We define volume in a YAML manifest where we define what pod to run:
```yaml
spec:
	container:
		- name: 
		  ...
		  volumeMounts:
            - name: pgdata
              mountPath: /bitnami/postgresql
    volumes:
  	  - name: pgdata
  	    emptyDir: {}
```
Such a volume allows to share data between containers in the same pod. It dies when the pod dies and data is lost.

Data is stored in the node's filesystem.