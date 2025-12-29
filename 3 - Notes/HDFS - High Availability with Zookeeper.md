Tags: [[__Data_Engineering]], [[__Distributed_computing]]

# Introduction
We can achieve a High Availability by having one Active NameNode and multiple Standby NameNodes.

Only the Active NameNode handles client requests and the other, Standby NameNodes are waiting to take over when the Active one fails.

Zookeeper can be used to monitor NameNodes and to replace a failed NameNode with another one.

#DataEngineering #DistributedComputing 