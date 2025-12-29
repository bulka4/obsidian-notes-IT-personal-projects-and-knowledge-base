Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]
#DeepSpeed #MLEngineering 

# Introduction
We can use the RayCluster CRD to prepare environment on Kubernetes ([[_Kubernetes|link]]) and submit many Ray Jobs which will use that environment to run multi-node, distributed DeepSpeed jobs. So that environment is reusable.

It ensures that all required pods, processes, environment variables, and networking are ready so that DeepSpeed (via PyTorch) can initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) and NCCL ([[NCCL|link]]) at runtime.
# How it works
We deploy a Ray cluster on Kubernetes and submit a training function/script to Ray Train. Ray handles:
- Preparing environment needed to use DeepSpeed
- Running a single DeepSpeed script or training function across multiple nodes

RayCluster CRD sets up the environment for DeepSpeed in the following way:
- Pod and cluster management
	- Uses a RayCluster CRD (or manually deployed Ray head and worker pods) on Kubernetes
	- Automatically schedules worker pods alongside the head pod, one pod per node using gang scheduling ([[Kubernetes - Gang scheduling|link]])
	    - Ensures all nodes are ready before initializing a DeepSpeed cluster
	- Manages the lifecycle of the Ray cluster: starts pods, restarts failed pods, and scales as needed
- Assigning roles and resources
    - Automatically distributes GPU resources across pods
    - Assigns roles internally via Ray (no explicit `master`/`worker` assignment required)
- Uses its own mechanism equivalent to `torchrun` launcher ([[PyTorch - The torchrun launcher|link]]) which:
	- Starts processes in each pod, one per GPU
	- Assigns proper values to environment variables:
		- `RANK`, `LOCAL_RANK`
		- `WORLD_SIZE`
		- `MASTER_ADDR`, `MASTER_PORT`
	- Initializes Torch Distributed process group using processes and env vars created earlier
- Performs setup needed for GPUs to communicate using NCCL (that communication will be used by DeepSpeed)

Then, we can submit Ray jobs which will run DeepSpeed jobs on that environment prepared by the RayCluster CRD.
# Pros and cons
For pros and cons of using Ray Train refer here - [[Ray Train - Pros and cons]].
# Other notes

# Questions
- How exactly do we submit a Ray job to run a script?
- what is Cleaner scaling and resource handling about? 