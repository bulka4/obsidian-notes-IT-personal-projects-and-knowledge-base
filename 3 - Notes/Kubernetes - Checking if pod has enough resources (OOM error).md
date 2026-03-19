Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
To check whether a pod was killed due to a OOM (out of memory) error, we check its description:
```bash
kubectl -n <namespace> describe pod <pod-name>
```
and look for `Reason: OOMKilled`.
# Watching memory usage live using bash
We can use bash to see memory usage live as described here - [[Linux & Bash - Watching memory usage live]].