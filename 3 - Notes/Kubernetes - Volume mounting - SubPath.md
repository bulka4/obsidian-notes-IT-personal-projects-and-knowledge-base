Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
We can use the subPath parameter in order to mount only a specific folder from a Volume.

For example below we mount:
- The ‘models’ folder from the Volume to the ‘/mnt/models’ folder in a Pod
- The ‘logs’ folder from the Volume to the ‘/mnt/logs’ folder in a Pod
```
volumeMounts:
	- name: azurefile
	  mountPath: /mnt/models
	  subPath: models
	- name: azurefile
	  mountPath: /mnt/logs
	  subPath: logs
```