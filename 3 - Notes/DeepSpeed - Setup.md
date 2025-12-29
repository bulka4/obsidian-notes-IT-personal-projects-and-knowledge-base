Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]
#DeepSpeed #MLEngineering 

# Introduction
To set up DeepSpeed for a distributed (multi-node) inference and training, we need to have:
- All the servers active when initialization starts
- Preparations for initializing a Torch Distributed process group ([[Torch Distributed process group|link]]), that is:
	- Set of processes, one per GPU, which will be performing DeepSpeed calculations
	- Environment variables created for each process RANK, LOCAL_RANK, WORLD_SIZE
	- Once we have those preparations, then every time we perform calculations using DeepSpeed, we will use them to initialize a process group
- Additional environment variables for each process:
	- MASTER_ADDR & MASTER_PORT (address and port of the master node)
- Prepare environment to enable NCCL communication
- Prepare pod networking & DNS so all nodes can reach the server given by the `MASTER_ADDR`
# Setting up on Kubernetes
Setting up on Kubernetes is described here - [[DeepSpeed - Setup on Kubernetes]].