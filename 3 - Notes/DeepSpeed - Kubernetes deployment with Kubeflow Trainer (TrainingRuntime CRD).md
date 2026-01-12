Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
TrainingRuntime CRD ([[Kubeflow Trainer - TrainingRuntime CRD|link]]) from the Kubeflow Trainer ([[Kubeflow Trainer - Introduction|link]]) can be used to perform an initial setup of a multi-node DeepSpeed cluster and run a container on Kubernetes ([[_Kubernetes|link]]).

Kubeflow Trainer is primarily meant for batch jobs, that is to run in a container a script which performs a fixed number of predictions and other operations, and finishes.

It also makes sense to use it for model serving ([[ML model serving - Multi-node vs single-node model running|link]]) but only when the model needs to be distributed across many nodes (computations for a single prediction needs to be distributed).

When our model can run on a single node, then that is not a good tool for that and it is better to use for example Ray Serve ([[Ray Serve - Introduction|link]]).

TrainingRuntime CRD ensures that all required pods, processes, environment variables, and networking are ready so that DeepSpeed (via PyTorch) can initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) and NCCL ([[NCCL|link]]) at runtime.
# Use cases and features
To learn more about use cases, features and when not to use TrainingRuntime CRD, refer to this document - [[Kubeflow Trainer - TrainingRuntime CRD use cases and features]].
# More about model serving
To learn more about serving models running in both a single-node and multi-node setup, refer to this document - [[ML model serving - Multi-node vs single-node model running]].
# How it works
We deploy a TrainingRuntime CRD and Kubeflow Trainer takes care of:
- Preparing environment needed to use DeepSpeed
- Running a DeepSpeed container

Preparing environment is done in the following way by the Kubeflow Trainer:
- Creating one pod ([[Kubernetes - Pod|link]]) per node using gang scheduling ([[Kubernetes - Gang scheduling|link]])
	- Initialization of a DeepSpeed cluster starts when all pods are ready, not earlier
- Manages job lifecycle
	- Creates the requested number of worker pods
	- Optionally restarts failed pods
	- Cleans up resources after the job finishes
- Assigns proper values to environment variables:
	- `RANK`, `LOCAL_RANK`
	- `WORLD_SIZE`
	- `MASTER_ADDR`, `MASTER_PORT`
- Runs the `deepspeed` command in every pod
	- That starts processes (one per GPU) which will be used to initialize a Torch Distributed process group
	- It uses env vars prepared earlier (`RANK` etc.)
# Setting up NCCL communication
DeepSpeed uses NCCL ([[NCCL|link]]) for communication between GPUs. To enable using NCCL in containers on Kubernetes, we can use NVIDIA GPU Operator like described here - [[NVIDIA GPU Operator]].
# Questions
- 