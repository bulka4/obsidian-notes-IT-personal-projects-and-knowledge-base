Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
We have the following processes (daemons, Java processes) running on nodes related to YARN:
-ResourceManager
-NodeManager
-ApplicationMaster
## ResourceManager
It is a global scheduler and resource allocator. It allocates containers on nodes which will be used by a process we want to run.

This process runs only on one node.
## NodeManager
Runs on each node, launches containers, monitors resources.
## ApplicationMaster
Every process we want to run with YARN (for example Spark jobs) gets its own ApplicationMaster.

It is responsible for:
-Requesting containers from the ResourceManager
-Requesting NodeManagers to launch containers

More information about how this works in case of Spark is in the ‘spark/spark on YARN notes’ document.

#DataEngineering #DistributedComputing #InfrastructureEngineering 