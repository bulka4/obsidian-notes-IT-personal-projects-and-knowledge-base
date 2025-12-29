Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
## Hadoop logs
We can check logs in the hadoop/logs folder.
## Start different processes separately
When running the start-dfs.sh from the master node it starts multiple processes on different nodes.

If some processes doesn’t want to start we can try to start this one process on one specific node.
## SSH and networking
Hadoop uses TCP for communication between nodes. We can test it by running:
- Ping \<hostname\>

Also we need to test passwordless ssh communication from the master node to all the slave nodes.

#DataEngineering #DistributedComputing 