Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
A persistent volume is a way to store data outside of a pod and keep that data even when pod dies. We specify here where data will be stored.

We create it as a separate resource and specify where the data will be stored:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
	capacity:
		storage: 5Gi
	accessModes:
		- ReadWriteOnce
	hostPath:
		path: /mnt/data # path on the node where data will be saved
```
