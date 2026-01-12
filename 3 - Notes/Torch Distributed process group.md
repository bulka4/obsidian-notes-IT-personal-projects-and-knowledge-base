Tags: [[_PyTorch]], [[__Machine_Learning_Engineering]]
#PyTorch #MLEngineering 

# Introduction
In order for Torch Distributed ([[Torch Distributed|link]]) to perform parallel calculations, we need to initialize a process group.

Processes in the group perform calculations and can use collective operations ([[Collective operations|link]]).

Creating a process group is done in the following way:
- We have a group of Python processes (can be on different servers, one process per GPU)
- Each process has access to environment variables:
	- `RANK` - Unique identifier of a process across all nodes
	- `LOCAL_RANK` - Unique identifier of a process on a single node
		- If there are multiple GPUs on one node, there are multiple processes on that node, one per GPU
		- `LOCAL_RANK` tells each process which GPU to use
	- `WORLD_SIZE` - World size, total number of all processes in the group
	- `MASTER_ADDR`, `MASTER_PORT` - IP address and port of the server we choose to be the master
	- They are needed to tell each process who it is, how many processes exist, and how to find them.
- Each process calls the `torch.distributed.init_process_group(...)` function

All processes meet at one known address (a master node given by the `MASTER_ADDR`, a rendezvous point), exchange information and then they can talk to each other.

When calling `torch.distributed.init_process_group(...)`, that function waits until all `WORLD_SIZE` processes has joined the process group.

For communication between processes on GPUs, NCCL ([[NCCL|link]]) is used. For communication with CPUs, Gloo is used.
# Preparing processes and env vars
To prepare processes and environment variables needed to initialize a process group using the `init_process_group` function, we can use different tools:
- The `torchrun` launcher ([[PyTorch - The torchrun launcher|link]])
- Ray Train API ([[Ray Train - API|link]])
- Kubeflow Trainer TrainingRuntime CRD ([[Kubeflow Trainer - TrainingRuntime CRD|link]])
- MPI Operator ([[MPI Operator|link]])