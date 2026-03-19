Tags: [[_Spark]] [[__Data_Engineering]] [[__Distributed_computing]]
#Spark #DataEngineering #DistributedComputing 

# Local mode
In a local mode, everything happens on a single server. When a client ([[Spark - Clients starting calculations|link]]) starts a Spark app, then workflow looks like this:
- Client starts a Spark driver ([[Spark - Components - Master, driver and executors|link]])
- Driver splits the app into tasks and sends them to executors to execute them

Driver is a logical object in a single JVM (Java virtual machine) and executors are threads inside the same JVM. That JVM can be either a part of our app process or a separate process.

There is no concept of a master in a local mode.
# Client mode
In a client mode, we use multiple servers (a multi-node cluster) and a resource manager (like YARN, Spark Standalone or Kubernetes) ([[Spark - Resource managers|link]]). Master ([[Spark - Components - Master, driver and executors|link]]) is a part of a resource manager.

When a client ([[Spark - Clients starting calculations|link]]) runs a Spark app, the workflow looks like this:
- The client starts a Spark driver on the same server
- The driver talks to the master and requests to create executor processes on nodes in a cluster
- The master starts executor processes
- The driver schedules tasks on those executors
# Cluster mode
In a cluster mode, like in the client mode, we use a multi-node cluster and a resource manager ([[Spark - Resource managers|link]]). Master ([[Spark - Components - Master, driver and executors|link]]) is a part of a resource manager.

When a client ([[Spark - Clients starting calculations|link]]) runs a Spark app, the workflow looks like this:
- The client submits the application to the master and requests to create a driver process
- The master creates a driver process (on any node in a cluster)
- Driver talks to the master and requests to create executor processes
- The master starts executor processes (on any node in a cluster)
- The driver schedules tasks on the executors
# Setting up a mode
In what mode Spark will run, depends on how we run Spark app. It is described here - [[Spark - Setting up a mode when using different clients]].
# Questions
- What are JVM threads?