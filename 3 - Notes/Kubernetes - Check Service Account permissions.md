Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Check whether a given service account has permissions for creating pods:
```bash
auth can-i create pods --as=system:serviceaccount:<namespace>:<service-account> -n <namespace>
```