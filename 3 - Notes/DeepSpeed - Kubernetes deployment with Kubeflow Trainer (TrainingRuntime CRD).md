Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]
#DeepSpeed #MLEngineering 

# Introduction
TrainingRuntime CRD ([[Kubeflow Trainer - TrainingRuntime CRD|link]]) from the Kubeflow Trainer ([[Kubeflow Trainer - Introduction|link]]) can be used to perform an initial setup and run a DeepSpeed job (a single script) on Kubernetes ([[_Kubernetes|link]]), on multiple nodes.

It ensures that all required pods, processes, environment variables, and networking are ready so that DeepSpeed (via PyTorch) can initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) and NCCL ([[NCCL|link]]) at runtime.
# How it works
We deploy a TrainingRuntime CRD and Kubeflow Trainer takes care of:
- Preparing environment needed to use DeepSpeed
- Running a single DeepSpeed script

It is one-time use, it prepares environment for DeepSpeed and runs only one script in that environment.

Preparing environment is done in the following way by the Kubeflow Trainer:
- Creating one pod ([[Kubernetes - Pod|link]]) per node using gang scheduling ([[Kubernetes - Gang scheduling|link]])
	- Initialization of a DeepSpeed cluster starts when all pods are ready, not earlier
	- Roles (`master`/`worker`) are automatically assigned by the CRD
- Manages job lifecycle
	- Creates the requested number of worker pods
	- Optionally restarts failed pods
	- Cleans up resources after the job finishes
- Assigns proper values to environment variables:
	- `RANK`, `LOCAL_RANK`
	- `WORLD_SIZE`
	- `MASTER_ADDR`, `MASTER_PORT`
- Runs `deepspeed` or `torchrun` commands in every pod
	- That starts processes (one per GPU) which will be used to initialize a Torch Distributed process group
	- It uses env vars prepared earlier (`RANK` etc.)
- Performs setup needed for GPUs to communicate using NCCL (that communication will be used by DeepSpeed)
# Questions
- 