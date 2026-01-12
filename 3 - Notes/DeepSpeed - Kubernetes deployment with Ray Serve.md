Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
Ray Serve can be used to set up a multi-node DeepSpeed cluster on Kubernetes and create a Rest API endpoint which will serve model's predictions done by DeepSpeed.

Although it is not recommended to use Ray Serve for setting up a multi-node cluster, where all the nodes need to cooperate with each other when performing distributed computations, like in case of DeepSpeed.

There are problems with that described later in this document in the 'Problems' section and 'Use cases and features'.

The best use case for Ray Serve is to run many pods, where each one can serve a model independently.
# Use cases and features
To learn more about use cases, features and when not to use Ray Train, refer to this document - [[Ray Serve - Use cases and features]].
# More about model serving
To learn more about serving models running in both a single-node and multi-node setup, refer to this document - [[ML model serving - Multi-node vs single-node model running]].
# Setting up a multi-node DeepSpeed cluster
When we deploy a RayService CRD, it creates pods which will run DeepSpeed processes (each pod runs one process for Torch Distributed process group) ([[DeepSpeed - Torch Distributed processes|link]]).

Ray actor replicas become processes which will form a Torch Distributed process group. Each of those replicas will set up necessary environment variables first before initializing a process group.
## Problems
It is possible to set up a multi-node DeepSpeed cluster using Ray Serve but in most situations that is not a good idea because:
- We need to set up manually environment variables on each pod with proper values, like `RANK` or `MASTER_ADDR` and it is complicated to do.
- When one node goes down, we need to restart all the nodes in the cluster to make DeepSpeed working again, while Ray Serve will restart only one node

Other tools, like:
- MPI operator ([[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]])
- Ray Train ([[DeepSpeed - Kubernetes deployment with Ray Train|link]])
- Kubeflow Trainer TrainingRuntime CRD ([[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]])
Can set up env vars automatically and restart all the pods in case of failure.
## Creating Pods
- RaySercice CRD creates Pods
	- On one pod, one deployment replica (actor) runs
	- Actor is a process used to form a Torch Distributed process group which will be used by DeepSpeed to perform calculations
- We specify number of Pods to create with the num_replicas variable in the Ray Serve deployment.
## Deployment and actors
Ray serve will create actors (processes) for a deployment (definition of Rest API endpoints), and those actors will execute the same deployment code.

Deployment code must:
- Set up env vars
- Initialize a torch process group
- Load a model using DeepSpeed

We need to have a static number of actor replicas since they initialize a DeepSpeed cluster. Otherwise, after adding or removing an actor, we would need to reinitialize a DeepSpeed cluster.
## Setting up env vars
### RANK
To get values for the `RANK` env vars, we can use replica context:
```python
from ray.serve.context import get_replica_context
        
@serve.deployment(...)
class deploymentName:
    def __init__(self):
    ...
	    
	ctx = get_replica_context()
	# ctx.replica_tag returns <deployment-name>#<replica-index>, where deployment-name in our case is deploymentName and replica-index are numbers starting from 0 which are unique for every actor replica created
	rank = int(ctx.replica_tag.split("#")[-1])
```
### MASTER_ADDR
To get value for `MASTER_ADDR`, we create a separate 'master' actor which will save this information as its attribute.

When creating replicas for the DeepSpeed deployment, the first replica (with rank 0) will create the master actor and save as its attribute the IP of the node where that first replica was created.

Other replicas will wait for the master actor to be created and read from it `MASTER_ADDR`.

Master actor:
```python
import ray

@ray.remote
class MasterInfo:
    def __init__(self):
        self.addr = None
        self.port = None

    def set(self, addr, port):
        self.addr = addr
        self.port = port

    def get(self):
        return self.addr, self.port
```

DeepSpeed deployment:
```python
import time
import ray
from ray import serve

@serve.deployment(...)
class DeepSpeedService:
    def __init__(self):
        # -------------------------
        # Create or get MasterInfo actor
        # -------------------------
        try:
	        # Find the master actor (MasterInfo) by its name if it exists
            master = ray.get_actor("ds_master")
        except ValueError:
	        # Create the master actor if it doesn't exist yet
            master = MasterInfo.options(
                name="ds_master",
                lifetime="detached"
            ).remote()

        # -------------------------
        # Rank 0 publishes master addr
        # -------------------------
        if rank == 0:
	        # Get IP of the node where the current actor replica is running
            master_addr = ray.util.get_node_ip_address()
            # Set IP as the master's IP (master_addr attribute)
            ray.get(master.set.remote(master_addr, MASTER_PORT))
        else:
            # Wait until master node is ready
            while True:
                addr, port = ray.get(master.get.remote())
                if addr is not None:
                    break
                time.sleep(0.5)
            master_addr = addr
```
### Local rank
Use one GPU per actor so we don't need to set up the `LOCAL_RANK` env var.
## Torch Distributed process group
We don't use `torchrun` to create processes which will form a Torch Distributed process group, Ray actors are those processes and each of them calls `init_process_group` to join the group.
## Loading a model
Each actors uses `deepspeed.init_inference` to load a model so it is distributed across nodes (if it is too big to fit on one node).
## NVIDIA GPU Operator
We need to use NVIDIA GPU Operator ([[NVIDIA GPU Operator|link]]) to enable using CUDA and NCCL in containers. 

It installs on the host:
- libraries:
	- NVIDIA driver ([[NVIDIA Driver|link]])
	- CUDA
	- NCCL
- NVIDIA Container Toolkit ([[NVIDIA Container Toolkit|link]])
- NVIDIA Device plugin (exposes GPUs to Kubetneres so pods can request, be scheduled on and access GPUs)

NVIDIA Container Toolkit is used by a container runtime (like docker, containerd) to inject (mount) NVIDIA driver ([[NVIDIA Driver|link]]), CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) libraries from the host into the container at runtime, allowing applications to use them in the container.

That allows applications in the container to perform calculations on GPUs.
## Code
Create an actor for saving information about the master node (its IP):
```python
import ray

# Actor with information about the master node. It needs to be an actor, not a normal class, so this data is saved in Ray object store and accessible from any node.
@ray.remote
class MasterInfo:
    def __init__(self):
        self.addr = None
        self.port = None

    def set(self, addr, port):
        self.addr = addr
        self.port = port

    def get(self):
        return self.addr, self.port
```

Create an actor for creating DeepSpeed cluster:
```python
import os
import time
import torch
import ray
import deepspeed

from ray import serve
from ray.serve.context import get_replica_context
from fastapi import FastAPI

app = FastAPI()
MASTER_PORT = 29500
WORLD_SIZE = 4  # MUST MATCH num_replicas

@serve.deployment(
    num_replicas=WORLD_SIZE,
    ray_actor_options={"num_gpus": 1}
)
@serve.ingress(app)
class DeepSpeedService:
    def __init__(self):
        self.initialized = False

    def _init_distributed(self):
        if self.initialized:
            return

        # -------------------------
        # Determine rank
        # -------------------------
        ctx = get_replica_context()
        # ctx.replica_tag returns <deployment-name>#<replica-index>, where deployment-name in our case is DeepSpeedService and replica-index are numbers starting from 0 which are unique for every actor replica created
        rank = int(ctx.replica_tag.split("#")[-1])

        # -------------------------
        # Create or get MasterInfo actor
        # -------------------------
        try:
	        # Find the master actor (MasterInfo) by its name if it exists
            master = ray.get_actor("ds_master")
        except ValueError:
	        # Create the master actor if it doesn't exist yet
            master = MasterInfo.options(
                name="ds_master",
                lifetime="detached"
            ).remote()

        # -------------------------
        # Rank 0 publishes master addr
        # -------------------------
        if rank == 0:
	        # Get IP of the node where the current actor replica is running
            master_addr = ray.util.get_node_ip_address()
            # Set IP as the master's IP (master_addr attribute)
            ray.get(master.set.remote(master_addr, MASTER_PORT))
        else:
            # Wait until master node is ready
            while True:
                addr, port = ray.get(master.get.remote())
                if addr is not None:
                    break
                time.sleep(0.5)
            master_addr = addr

        # -------------------------
        # Set env vars
        # -------------------------
        os.environ["RANK"] = str(rank)
        os.environ["LOCAL_RANK"] = "0"  # per-GPU rank in actor (adjust if multiple GPUs per actor)
        os.environ["WORLD_SIZE"] = str(WORLD_SIZE)
        os.environ["MASTER_ADDR"] = master_addr
        os.environ["MASTER_PORT"] = str(MASTER_PORT)

        torch.cuda.set_device(0)

        # -------------------------
        # Init torch process group
        # -------------------------
        torch.distributed.init_process_group(
            backend="nccl",
            rank=rank,
            world_size=WORLD_SIZE,
        )

        # -------------------------
        # Init DeepSpeed inference
        # -------------------------
        self.model = deepspeed.init_inference(
            model=load_your_model_here(),
            mp_size=WORLD_SIZE,
            dtype=torch.float16,
            replace_method="auto",
        )

        self.initialized = True

    @app.get("/generate")
    async def generate(self, prompt: str):
        self._init_distributed()
        with torch.no_grad():
            return self.model.generate(prompt)
```
# Questions
- 