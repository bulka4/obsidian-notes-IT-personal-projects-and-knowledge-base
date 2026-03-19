Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Delete a resource:
```bash
Kubectl delete <resource-type> <resource-name>
```

Edit a resource:
- Using a chosen editor in terminal (nano in this example):
	```bash
	EDITOR=nano kubectl edit <resource-type> <resource-name>
	```
- Edit a resource by executing a single command and providing a pattern what to change:
	```bash
	Kubectl patch <resource-type> <resource-name> --patch '<patch-data>' 
	[options]
	```

Deploy a resource using its YAML manifest:
```bash
kubectl apply -f manifest.yaml
```
	