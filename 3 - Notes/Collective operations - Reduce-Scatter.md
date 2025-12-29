Tags: [[__Distributed_computing]]
#DistributedComputing 

# Introduction
Reduce-Scatter is one of collective operations ([[Collective operations|link]]) where we combine tensors from all processes (like in all-reduce ([[Collective operations - All-Reduce|link]])), but scatter pieces back so each process gets a part of the result:
$$
\large \text{all\_gather} (x_1, \ldots, x_n) \rightarrow [y_1, \ldots, y_n]
$$
where:
- $x_1, \ldots, x_n$ - Outputs from nodes / GPUs
- Results $y_i$ are sent back to the $i$-th node / GPU