Tags: [[_PyTorch]], [[__Machine_Learning_Engineering]]
#PyTorch #MLEngineering 

# Introduction
DistributedDataParallel (DDP) is a high-level PyTorch API that simplifies distributed training by automatically performing gradient synchronization across multiple GPUs using collective operations (like `all_reduce`) ([[Collective operations|link]]).

Tools like DDP are called a 'distributed training abstraction' because it abstracts away basic Torch Distributed collective communication primitives (operations).
# How it works
DDP uses processes created by the `torchrun` command ([[PyTorch - The torchrun launcher|link]]), i.e. one process per GPU.

Each process has a full copy of the model and part of data used, and performs calculations only on that data subset. Results are then gathered and synchronized.
# Questions
- 