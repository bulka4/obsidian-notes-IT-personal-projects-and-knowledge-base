Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Volumes are a resource which works like volumes in Docker. Volumes allow us to save data from a container outside of a container (on a host running a container).

So container will be using this data and even after container restart, that data will be still accessible.

Volumes need to be used together with VolumeMounts which will specify the path in the container where data from a Volume will be accessible.

We can additionally use the hostPath parameter to specify where data from a Volume will be stored on a host.
## Volume defined in the resource where it will be mounted
We can create a Volume in the same YAML manifest where we create a resource into which will mount this Volume.

For example such a YAML manifest might look like this:
![[2 - Images/Kubernetes/Screenshot 8.png]]
## Volume created as a separate resource
The other way of creating a Volume is to create a separate Volume resource.

Except for creating just a Volume we need to create additionally a Volume claim.

When we want to mount this Volume to a Pod, we are using the Volume claim in the Pod’s specification.

Here is an example of mounting a Persistent Volume (it preserves data even after Pod is deleted) to a Pod:
![[2 - Images/Kubernetes/Screenshot 9.png]]
## Volume with configMap
We can use a configMap to create a volume and mount it to a Pod.

This way in the path inside the container specified by the ‘mountPath’ parameter we are creating:
- A file for each item from the ConfigMap
- Each file has the same name as name of the key from the ConfigMap item
- Each file called ‘key-name’ has content equal to value from ConfigMap corresponding to the key called ‘key-name’

So for example if we create a ConfigMap by reading content of a file:
![[2 - Images/Kubernetes/Screenshot 10.png]]

So here we create an item in ConfigMap with key-name = ‘filename.txt’ and value for that key is a content of the /home/username/filename.txt file.

And then we create a Volume and volumeMount like this:
![[2 - Images/Kubernetes/Screenshot 11.png]]

Then inside that container we can access the content of the /home/username/filename.txt under the /etc/config/filename.txt path.
## Volume claims
As mentioned earlier in the ‘Volumes and volumeMounts’ section, we can use Volume claims in order to attach a Volume to our Pod.

If we deploy a Volume claim, then we need to have either a volume prepared or we need to have a dynamic storage provisioner which is explained in another section.
## Dynamic storage provisioner
A Dynamic storage provisioner automatically creates a volume when a volume claim is deployed.

An example of a dynamic storage provisioner is the StorageClass resource. It can be used for example to automatically create a disk in Azure used to store volume’s data.
## SubPath
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


#Cloud #DevOps #DistributedComputing #DataEngineering 