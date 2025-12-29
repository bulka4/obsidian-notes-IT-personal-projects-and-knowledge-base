Tags: [[_PyTorch]], [[__Machine_Learning_Engineering]]
#PyTorch #MLEngineering 

# Introduction
Torch Distributed (`torch.distributed`) is PyTorch’s distributed computing library. It allows to run a ML model across multiple GPUs and/or multiple nodes (servers), handling:
- Communication between GPUs (in different nodes or in the same node)
- Collective operations ([[Collective operations|link]])
	- They are used to synchronize model parameters or gradients during distributed training.
# Tools
Torch Distributed provides the following tools and features:
- Process group initialization (`init_process_group` ([[Torch Distributed process group|link]]))
- Collective communication primitives (`all_reduce`, `broadcast`, `all_gather`, etc.)
- Distributed training abstractions (like `DistributedDataParallel` ([[PyTorch - DistributedDataParallel (DDP)|link]]), RPC, etc.)
- Backend support (it is compatible with communication frameworks like NCCL ([[NCCL|link]]), Gloo, MPI ([[MPI (Message Passing Interface)|link]]))
# Questions
- What does it mean that it is compatible with communication frameworks?
- 