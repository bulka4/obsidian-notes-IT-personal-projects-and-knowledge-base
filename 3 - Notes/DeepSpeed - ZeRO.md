Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
ZeRO stands for Zero Redundancy Optimizer. It is used for inference (making predictions) and training models (mainly neural networks) using gradient-based optimizers, like Adam ([[Adam optimizer|link]]) or Gradient Descent ([[Gradient Descent - ML|link]]). 

It helps with performing big calculations, which happens in gradient-based optimizers, by partitioning tensors ([[Tensor|link]]) across multiple GPUs (can be on different servers). Each GPU performs calculations only on a subset of all the numbers.
# Stages
There are 3 stages to choose which we want to use, each of them partitions different subsets of numbers:
- Stage 1 – Splits optimizer states (additional tensors used in the optimizer, different than model parameters, for example vectors $m_t, v_t$ in Adam)
- Stage 2 – Splits optimizer states and gradients
- Stage 3 – Splits optimizer states, gradients and model’s parameters (weights)

So Stage 3 includes Stage 2 and Stage 2 includes Stage 1.
# Communication
To perform calculations, GPUs need to communicate with each other as explained here - [[DeepSpeed - Communication between GPUs|link]].

More numbers we partition across GPUs (the higher stage we use), the bigger communication overhead we have.
# ZeRO-Offload
ZeRO-Offload is a functionality to offload GPUs. It allows to use CPUs and RAM for storing numbers which are not currently needed GPUs for calculations.
# ZeRO-Infinity
ZeRO-Infinity extends functionality of the ZeRO-Offload by using not only CPUs and RAM but also NVMe (disk) to offload GPUs by storing numbers which are not currently used by GPUs for calculations.

#DistributedComputing #MLEngineering 