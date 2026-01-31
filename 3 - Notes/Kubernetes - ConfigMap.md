Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
ConfigMap is a resource which we can use to provide an external configuration for an application running as a container in a Pod.

We can store there data as key value pairs which will be used by our app running in Pod, and we can change them without changing the app itself.
# Mounting a file
We can use ConfigMap to create a file with specified content and mount it into a pod:

ConfigMap:
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

Mount it into a pod:
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