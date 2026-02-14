Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
If we are running multiple containers in the same pod, then they share a namespace ([[Linux & bash - Namespaces]]) (network configs, PID ([[Linux - Processes|link]])). 

For example in one container we can list processes which are running and it will include processes from another container.