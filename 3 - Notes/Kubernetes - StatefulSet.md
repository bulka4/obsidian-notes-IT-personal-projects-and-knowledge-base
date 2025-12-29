Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
It is like a Deployment but specifically designed for applications which have a state. For example databases have a state which is their data (which changes over time). We can’t simply delete and recreate such an app because we will loose that state.

Even if we are using volumes for our databases running in Pods, then still we should use the StatefulSet for them to guarantee data consistency.

#Cloud #DevOps #DistributedComputing #DataEngineering 