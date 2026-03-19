Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
We can use `describe` command to get info about deployed pod, including:
- Pod specification
- Status
- Events
```bash
kubectl -n <namespace> describe pod <pod-name>
```