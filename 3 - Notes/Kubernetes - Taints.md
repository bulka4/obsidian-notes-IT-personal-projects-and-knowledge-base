Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Taints are a way to control which Pods can be scheduled on which Nodes.

We can create a taint on a Node and then every Pod that doesn’t tolerate it will not be able to be scheduled on that Node.
# Key, value and effect
Every Taint consists of 3 parts: key, value and effect:
- Key and value identifies a Taint (unique identifier of a Taint)
- Effect defines what happens when we try to schedule a Pod on a Node that has a Taint not tolerated by that Pod.
# Creating a taint
We can create a taint like this:
```
kubectl taint nodes <node-name> gpu=true:NoSchedule
```
here:
- 'gpu' is the key
- 'true' is the value
- 'NoSchedule' is the effect
# Tolerating a taint in pod's manifest
In a pod’s manifest, we can specify which taints it tolerates and then we can create that pod on nodes which have those taints.

For example, if we have a taint like this:
```
gpu=true:NoSchedule
```
Then, in pod's manifest, we can declare that this pod will tolerate it like this:
```yaml
tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
```

#Cloud #DevOps #DistributedComputing #DataEngineering 