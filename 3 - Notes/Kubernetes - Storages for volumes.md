Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When choosing a storage for a PV (persistent volume), we need to consider whether we will need to set up POSIX permissions ([[Kubernetes - Volume mounting -  File permissions|link]]) and what access mode do we need ([[Kubernetes - PVC access modes|link]]).

Below table describes which storages supports POSIX permissions and whether or not they support the RWX access mode:

| Storage          | POSIX ACL | RWX access mode |
| ---------------- | --------- | --------------- |
| Azure File Share | no        | yes             |
| Azure ADLS Gen2  | yes       | no              |
