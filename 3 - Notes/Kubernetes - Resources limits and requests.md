Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
In manifests, we can set up:
- Resource limits - How much resources can be used maximally
- Resource requests - How much resources need to be available

If amount of available resources is lower than what is requested => pod will not be scheduled.

If pod wants to use more resources than what is set up in its limit => pod will get killed and restarted.

When we set up only a limit and not a request, then request is automatically set up to the same value as limit.