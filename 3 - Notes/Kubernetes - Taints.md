Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Taints are a way to control which Pods can be scheduled on which Nodes.

We can create a taint on a Node and then every Pod that doesn’t tolerate it will not be able to be scheduled on that Node.

In a Pod’s manifest we can specify which taints it tolerates and then we can create that Pod on Nodes which have those taints.

Every Taint consists of 3 parts: key, value and effect. Key and value identifies a Taint (unique identifier of a Taint) and effect defines what happnes when we try to schedule a Pod on a Node that has a Taint not tolerated by that Pod.

#Cloud #DevOps #DistributedComputing #DataEngineering 