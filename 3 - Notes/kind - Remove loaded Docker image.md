Tags: [[_kind]] [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#kind #Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
- Check cluster name: 
	```bash
	kind get clusters
	```
- Check images loaded to the kind cluster:
  ```bash
	docker exec <kind-cluster-name>-control-plane circtl images
  ```
- Remove an image:
  ```bash
	docker exec <kind-cluster-name>-control-plane circtl rmi <image-name>
  ```