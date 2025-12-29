Tags: [[__Distributed_computing]]
#DistributedComputing 

# Introduction
All-Reduce is one of collective operations ([[Collective operations|link]]) where we get outputs from all the nodes / GPUs and perform on them some operation which returns a single number:
$$
\large \text{all\_reduce} (x_1, \ldots, x_n) \rightarrow y
$$
where:
- all_reduce - Some operation, like adding, selecting a max etc.
- $x_1, \ldots, x_n$ - Outputs from nodes / GPUs

The output $y$ is sent back to all the nodes / GPUs to continue calculations.