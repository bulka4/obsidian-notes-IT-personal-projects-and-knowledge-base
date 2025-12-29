Tags: [[__Distributed_computing]]
#DistributedComputing 

# Introduction
All-Gather is one of collective operations ([[Collective operations|link]]) where we collect tensors ([[Tensor|link]]) from all nodes / GPUs and concatenates them:
$$
\large \text{all\_gather} (x_1, \ldots, x_n) \rightarrow y = [x_1, \ldots, x_n]
$$
where:
- $x_1, \ldots, x_n$ - Outputs from nodes / GPUs

The output $y$ is sent back to all the nodes / GPUs to continue calculations.