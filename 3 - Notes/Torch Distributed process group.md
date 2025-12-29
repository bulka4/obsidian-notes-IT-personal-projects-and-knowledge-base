Tags: [[_PyTorch]], [[__Machine_Learning_Engineering]]
#PyTorch #MLEngineering 

# Introduction
In order for Torch Distributed ([[Torch Distributed|link]]) to perform parallel calculations, we need to initialize a process group.

It is done using the the `init_process_group` function and it requires:
- A group of processes - They can run on different servers
- Environment variables defined for each process which will be used for communication between them:
	- RANK, LOCAL_RANK - Global and local rank of the process which are unique identifiers
	-  WORLD_SIZE - World size, total number of all processes in the group

Processes in the group can use collective operations ([[Collective operations|link]]).

For communication between processes on GPUs, NCCL is used. For communication with CPU, Gloo is used.
# Preparing processes and env vars
To prepare processes and environment variables needed to initialize a process group using the `init_process_group` function, we can use different tools:
- The `torchrun` launcher ([[PyTorch - The torchrun launcher|link]])
- Ray Train
- Kubeflow Trainer TrainingRuntime CRD ([[Kubeflow Trainer - TrainingRuntime CRD|link]])
- MPI Operator ([[MPI Operator|link]])