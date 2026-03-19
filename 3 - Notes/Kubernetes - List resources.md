Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
List resources of a specific type:
- In a specific namespace:
	```bash
	Kubectl get <resource-type> -n <namespace>
	```
- In all namespaces:
  ```bash
	kubectl get <resource-type> -n --all-namespaces
  ```
