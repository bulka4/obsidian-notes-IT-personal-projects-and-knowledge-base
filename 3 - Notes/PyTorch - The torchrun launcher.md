Tags: [[_PyTorch]], [[__Machine_Learning_Engineering]]
#PyTorch #MLEngineering 

# Introduction
The `torchrun` launcher is a command to launch processes and set up environment variables on a single server needed for communication between those processes. Those processes can be then used to create a Torch Distributed process group ([[Torch Distributed process group|link]]).

The `torchrun` launcher performs the following tasks:
- Starts one process per GPU
- Sets environment variables if they are not already present: RANK, LOCAL_RANK, WORLD_SIZE
where:
- The RANK and LOCAL_RANK env vars are unique identifiers of each process
- The WORLD_SIZE env var is a total number of processes

Those env vars are needed for communication between those processes which are responsible for running our Python code, which then runs PyTorch code, which uses tools from Torch Distributed ([[Torch Distributed|link]]) to perform distributed calculations.

Instructions followed in the process of launching PyTorch processes using the `torchrun` command are called 'torch-distributed runtime'.
# Questions
- 