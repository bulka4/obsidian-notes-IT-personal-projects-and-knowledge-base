Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Gang scheduling is a technique used in Kubernetes ([[_Kubernetes|link]]) to start all the pods at the same time. 

Pods can be created at different times but we don't run on them any process until all pods are ready. Once all pods are prepared, processes start on them.

This is needed for example in distributed computing ([[__Distributed_computing|link]]) when multiple pods cooperate with each other.

Kubernetes doesn't support it natively but there is a lot of tools which enable gang scheduling.