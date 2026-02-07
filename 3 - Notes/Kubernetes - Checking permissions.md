Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
We can check if given identity (service account, user, group etc) has a permission for performing a given action.

For example, we can check if one pod can create other pods using given service account:
```bash
kubectl auth can-i create pods -n <namespace> \
  --as=system:serviceaccount:<namespace>:<service-account-name>
```
