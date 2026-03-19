Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
API server talks to the Scheduler and Scheduler decides on which node to run requested Pods. It check how much resources (CPU, RAM) will be needed for running a Pod, and which nodes have those resources available.

Scheduler doesn’t run the app itself but it talks to the kubelet and kubelet runs an app.