Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
TCP communication between processes is used only at the beginning, when initializing a cluster.

After that, processes talk to each other over NCCL to exchange data needed for calculations.

#DistributedComputing #MLEngineering 