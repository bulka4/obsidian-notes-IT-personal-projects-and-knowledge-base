Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]
#DistributedComputing #MLEngineering 

# Introduction
Pipeline parallelism is a technique where we split calculations for neural network layers ([[Neural Network|link]]) across GPUs, so each GPU calculates only a subset of all the layers, for example:
- GPU 1 calculates layers 1 - 3
- GPU 2 calculates layers 4 - 6

Tensor parallelism is a technique where we split calculations happing inside of a single layer across GPUs. For example, if we need to add vectors in a layer:
$$
[1,2] + [1,2]
$$
then:
- GPU 1 can calculate addition for the first element: 1 + 1 = 2
- GPU 2 can calculate addition for the second element: 2 + 2 = 4

It is used for both training models and inference (making predictions).
# Comparison to ZeRO
In ZeRO partitioning ([[DeepSpeed - ZeRO|link]]), we also split calculations across GPUs, for example if we want to add vectors:
$$
[1,2] + [1,2]
$$
then both methods, ZeRO and tensor parallelism can split calculations like this:
- GPU 1 can calculate addition for the first element: 1 + 1 = 2
- GPU 2 can calculate addition for the second element: 2 + 2 = 4

But the difference is in data which each GPU stores:
- In ZeRO, data is split, GPU 1 stores only two values 1 and 1
- In tensor parallelism, data is not split, both GPUs stored the entire vectors [1, 2], [1, 2].

When data can fit on a single GPU, then we don't need need ZeRO but tensor parallelism might be useful, since even though data fits on a single GPU, it might not be able to perform all the calculations on that data in parallel. 

By splitting calculations across many GPUs using tensor parallelism, we might be able to perform all the calculations in parallel.

When data doesn't fit on one GPU, then we need to use ZeRO and using tensor parallelism additionally might speed up calculations additionally like described earlier.

Splitting data too much using ZeRO is not good because then, GPUs need to communicate with each other more frequently to exchange data and results of operations, what slows down computations.

So sometimes it is better to split only computations using tensor parallelism without splitting data further using ZeRO in order to avoid communication overhead.

#DistributedComputing #MLEngineering 