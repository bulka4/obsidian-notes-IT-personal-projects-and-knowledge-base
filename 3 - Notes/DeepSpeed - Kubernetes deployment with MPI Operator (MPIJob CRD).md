Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]]

# Introduction
MPI operator ([[MPI Operator|link]]) can be used to perform an initial setup and run a DeepSpeed job (a single script) on Kubernetes ([[_Kubernetes|link]]), on multiple nodes.

It ensures that all required pods, processes, environment variables, and networking are ready so that DeepSpeed (via PyTorch) can initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) and NCCL ([[NCCL|link]]) at runtime.
# How it works
We deploy a MPIJob CRD ([[Kubernetes - CRD|link]]) and MPI operator takes care of:
- Preparing environment needed to use DeepSpeed
- Running a single DeepSpeed script

It is one-time use, it prepares environment and runs only one DeepSpeed script in that environment.

Preparing environment is done in the following way:
- Creating one pod ([[Kubernetes - Pod|link]]) per node using gang scheduling ([[Kubernetes - Gang scheduling|link]])
	- Initialization of a DeepSpeed cluster starts when all pods are ready, not earlier
	- One pod is the 'Launcher' pod that runs the `mpirun` command ([[MPI - The mpirun command|link]]) together with `deepspeed` or `torchrun` ([[PyTorch - The torchrun launcher|link]]) commands (e.g. `mpirun torchrun`)
	- Other pods are 'Workers' that run calculations
- Managing job lifecycle
	- Creates the requested number of worker pods
	- Optionally restarts failed pods
	- Cleans up resources after the job finishes

The `mpirun torchrun` command (the same for `mpirun deepspeed`), which we run on the Launcher pod, performs following tasks:
- Sets up communication
	- Prepares environment allowing GPUs and CPUs to exchange data across nodes
	- Thanks to that, DeepSpeed can initialize and use NCCL ([[DeepSpeed - NCCL|link]])
- Sets environment variables which will be used by the `torchrun` command:
	- `OMPI_COMM_WORLD_RANK`
	- `OMPI_COMM_WORLD_LOCAL_RANK`
	- `OMPI_COMM_WORLD_SIZE`
	- `OMPI_COMM_WORLD_MASTER_ADDR
	- `OMPI_COMM_WORLD_MASTER_PORT
- Runs `torchrun` in every pod

The `mpirun` command uses the MPI ([[MPI (Message Passing Interface)|link]]) communication when performing those tasks.

Then, we need to map those env vars prepared by `mpirun` into env vars required by the `torchrun` (by writing our own bash script):
- `RANK` -> `OMPI_COMM_WORLD_RANK`
- `LOCAL_RANK` -> `OMPI_COMM_WORLD_LOCAL_RANK`
- `WORLD_SIZE` -> `OMPI_COMM_WORLD_SIZE`
- `MASTER_ADDR` -> `OMPI_COMM_WORLD_MASTER_ADDR
- `MASTER_PORT` -> `OMPI_COMM_WORLD_MASTER_PORT

The `torchrun` command, which is ran in every pod, performs preparations to initialize a Torch Distributed process group ([[Torch Distributed process group|link]]):
- Starts one process per GPU
- Uses env vars which we prepared
# Questions
- 