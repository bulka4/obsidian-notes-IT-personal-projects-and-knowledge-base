Tags: [[_Spark]] [[__Data_Engineering]] [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Introduction
The main components (which are processes) of Spark are:
- Master - A coordinator of other processes. It creates the driver and executor processes and allocates resources to them (CPU, RAM).
- Driver - A task coordinator, it prepares tasks to execute, to produce the final output and sends tasks to executors.
- Executors - execute tasks sent by the driver.
# Master and resource managers
For Spark, we need choose a resource manager and master is a part of a resource manager. 

So what process exactly plays the role of the master depends on what resource manager we choose. More about resource managers for Spark can be found here - [[Spark - Resource managers]].
# Master and Spark modes
Spark can be run in different modes. More about Spark modes can be found here - [[Spark - Modes]].

- When we run Spark in a local mode, then there is no master.
- When we run Spark in a client or cluster mode, then we use multiple servers and master can start processes on any of them.