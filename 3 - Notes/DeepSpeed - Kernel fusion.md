Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# What is kernel fusion
Kernel fusion is the process of combining multiple small GPU operations into a single GPU kernel ([[GPU kernel and threads|link]]).

GPUs are very fast at running a single large kernel, but launching many small kernels adds overhead and reduces efficiency.

- In deep learning, many operations (like element-wise additions, layer normalization, activation functions) are often applied sequentially
- Each operation alone might launch its own GPU kernel → slow due to kernel launch overhead
- By fusing operations, DeepSpeed can execute them in one kernel, reducing launch overhead and increasing GPU utilization
# Kernel fusion in DeepSpeed
DeepSpeed doesn't have a functionality to automatically combine functions written by us into a single kernel but it uses kernel fusion internally. 

That means, it provides kernels for us to use, which include many operations in that single kernel, instead of providing only separated kernels for each operation.
# Attention layer example
For example, kernel fusion is used to avoid using multiple kernels for operations happening in an attention layer in neural network ([[Neural Network - Attention layer|link]]).

For example:
- Instead of calculating separately $y = QK^T$ and $\text{softmax}(y)$ in separate kernels, they are calculated in one kernel
- In multi-head attention ([[Neural Network - Multi-Head Attention (MHA) layer|link]]), calculating $Q_h k_h^T$ for each head $h$ happens in the same kernel instead of separate ones
# Questions


#DistributedComputing #MLEngineering 