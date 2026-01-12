Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
MPI operator ([[MPI Operator|link]]) can be used to perform an initial setup of multi-node DeepSpeed cluster and run a container on Kubernetes ([[_Kubernetes|link]]).

MPI operator is primarily meant for batch jobs, that is to run in a container a script which performs a fixed number of predictions and other operations, and finishes.

It also makes sense to use it for model serving ([[ML model serving - Multi-node vs single-node model running|link]]) but only when the model needs to be distributed across many nodes (computations for a single prediction needs to be distributed).

When our model can run on a single node, then that is not a good tool for that and it is better to use for example Ray Serve ([[Ray Serve - Introduction|link]]).

MPI operator ensures that all required pods, processes, environment variables, and networking are ready so that DeepSpeed (via PyTorch) can initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) and NCCL ([[NCCL|link]]) at runtime.
# Use cases and features
To learn more about use cases, features and when not to use MPI Operator, refer to this document - [[MPI Operator - Use cases and features]].
# More about model serving
To learn more about serving models running in both a single-node and multi-node setup, refer to this document - [[ML model serving - Multi-node vs single-node model running]].
# How it works
We deploy a MPIJob CRD ([[Kubernetes - CRD|link]]) and MPI operator takes care of:
- Preparing environment needed to use DeepSpeed
- Running a DeepSpeed container

Preparing environment is done in the following way:
- Creating one pod ([[Kubernetes - Pod|link]]) per node using gang scheduling ([[Kubernetes - Gang scheduling|link]])
	- Initialization of a DeepSpeed cluster starts when all pods are ready, not earlier
	- One pod is the 'Launcher' pod that runs the `mpirun` command ([[MPI - The mpirun command|link]])
	- Other pods are 'Workers' that run calculations
- Managing job lifecycle
	- Creates the requested number of worker pods
	- Optionally restarts failed pods
	- Cleans up resources after the job finishes

The `mpirun` command, which we run on the Launcher pod, needs to be used together with another bash script.

So we run `mpirun ./entrypoint.sh` where `./entrypoint.sh` looks like this:
```shell
export RANK=$OMPI_COMM_WORLD_RANK
export LOCAL_RANK=$OMPI_COMM_WORLD_LOCAL_RANK
export WORLD_SIZE=$OMPI_COMM_WORLD_SIZE
export MASTER_ADDR=$OMPI_COMM_WORLD_MASTER_ADDR
export MASTER_PORT=$OMPI_COMM_WORLD_MASTER_PORT

exec torchrun ...
```

Below is explained how `mpirun ./entrypoint.sh` works:

The `mpirun` command, for every pod:
- Sets environment variables which will be used by the `torchrun` command:
	- `OMPI_COMM_WORLD_RANK`
	- `OMPI_COMM_WORLD_LOCAL_RANK`
	- `OMPI_COMM_WORLD_SIZE`
	- `OMPI_COMM_WORLD_MASTER_ADDR
	- `OMPI_COMM_WORLD_MASTER_PORT
- Those env vars are mapped by our bash script into env vars needed for the `torchrun` command:
	- `RANK` -> `OMPI_COMM_WORLD_RANK`
	- `LOCAL_RANK` -> `OMPI_COMM_WORLD_LOCAL_RANK`
	- `WORLD_SIZE` -> `OMPI_COMM_WORLD_SIZE`
	- `MASTER_ADDR` -> `OMPI_COMM_WORLD_MASTER_ADDR`
	- `MASTER_PORT` -> `OMPI_COMM_WORLD_MASTER_PORT`
- Runs `torchrun`

The `torchrun` command performs preparations to initialize a Torch Distributed process group ([[Torch Distributed process group|link]]):
- Uses env vars which we prepared
- Starts one process per GPU

So `mpirun` helps us with setting up proper values for env vars and running `torchrun` on every pod.
# Setting up NCCL communication
DeepSpeed uses NCCL ([[NCCL|link]]) for communication between GPUs. To enable using NCCL in containers on Kubernetes, we can use NVIDIA GPU Operator like described here - [[NVIDIA GPU Operator]].
# Questions
- 