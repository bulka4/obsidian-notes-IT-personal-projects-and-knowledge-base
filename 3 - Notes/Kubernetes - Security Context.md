Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When creating a pod or deployment, we can specify:
```yaml
securityContext: 
	runAsUser: 185
	runAsGroup: 185
	fsGroup: 185
```
that means, that:
- `runAsUser: 185` & `runAsGroup: 185` - Process in the container will be started as the user with ID=185 who belongs to the user group with ID=185
- `fsGroup: 185` - All the mounted folders will be writable by users from the group with ID=185
	- It doesnt work for all the volumes, it works for:
		- `emptyDir`
	    - `persistentVolumeClaim` (most CSI drivers)
	- But doesn't work for:
		- `hostPath`
		- some NFS setups
		- certain CSI drivers that disable it