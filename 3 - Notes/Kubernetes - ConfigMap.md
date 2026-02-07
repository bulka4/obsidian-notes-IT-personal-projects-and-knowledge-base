Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
ConfigMap is a resource which we can use to provide an external configuration for an application running as a container in a Pod.

We can store there data as key value pairs which will be used by our app running in Pod, and we can change them without changing the app itself.
# Creating a content of a file
We can create a ConfigMap which stores a content of a file. It can be later mounted into a pod to make that file available in the pod's filesystem.
## Defining content in a manifest
We can define a content of a file in a YAML manifest where we create a ConfigMap:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: config-filename
data:
  filename.xml: |
    <configuration>
    ...
```
## Reading content from an existing file
We can also create a file content in a ConfigMap by reading an existing file:
```bash
kubectl create configmap my-config \
	--from-file=filename.txt=/path/to/file.txt
```
where `/path/to/file.txt` is the local path.
# Mounting into a pod
Once we have a ConfigMap with a content of a file, we can mount it into a pod to make that file available in the pod's filesystem:
```yaml
apiVersion: apps/v1
kind: Deployment
...
spec:
	...
	template:
		...
		spec:
		    containers:
			    ...
			    volumeMounts:
	            - name: volume-name
	              mountPath: /path/filename
	              subPath: filename
		    volumes:
		        - name: volume-name
		          configMap:
		            name: filename
```

In this case, data (file content from the ConfigMap) is saved in etcd. Creating a volume doesn't create a separate storage (like PVC). 

We can mount this way one ConfigMap to many pods and no data will be duplicated on a disk.

#Cloud #DevOps #DistributedComputing #DataEngineering 