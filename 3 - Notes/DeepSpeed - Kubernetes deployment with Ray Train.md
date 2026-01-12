Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
We can use the RayCluster CRD to prepare environment on Kubernetes ([[_Kubernetes|link]]) and submit many jobs using Ray Train API ([[Ray Train - API|link]]) which will use that environment to run multi-node, distributed DeepSpeed jobs.

Ray Train API is primarily meant for batch jobs, that is to run in a function which performs a fixed number of predictions and other operations, and finishes.

It also makes sense to use it for model serving ([[ML model serving - Multi-node vs single-node model running|link]]) but only when the model needs to be distributed across many nodes (computations for a single prediction needs to be distributed).

When our model can run on a single node, then that is not a good tool for that and it is better to use for example Ray Serve ([[Ray Serve - Introduction|link]]).

RayCluster CRD and Ray Train API ensure that all required pods, processes, environment variables, and networking are ready so that DeepSpeed (via PyTorch) can initialize a Torch Distributed process group ([[Torch Distributed process group|link]]) and NCCL ([[NCCL|link]]) at runtime.
# Use cases and features
To learn more about use cases, features and when not to use Ray Train, refer to this document - [[Ray Train - Use cases and features]].
# More about model serving
To learn more about serving models running in both a single-node and multi-node setup, refer to this document - [[ML model serving - Multi-node vs single-node model running]].
# How it works
Using RayCluster CRD we prepare pods and using Ray Train API we create a Python function which after execution initializes a Torch Distributed process group and runs DeepSpeed code in a distributed way across many pods.

RayCluster CRD sets up the environment for DeepSpeed in the following way:
- Pod and cluster management
	- Uses a RayCluster CRD (or manually deployed Ray head and worker pods) on Kubernetes
	- Automatically schedules worker pods alongside the head pod, one pod per node using gang scheduling ([[Kubernetes - Gang scheduling|link]])
	    - Ensures all nodes are ready before initializing a DeepSpeed cluster
	- Manages the lifecycle of the Ray cluster: starts pods, restarts failed pods, and scales as needed
- Assigning resources
    - Automatically distributes GPU resources across pods

Ray Trainer API ([[Ray Train - API|link]]) uses its own mechanism equivalent to `torchrun` launcher ([[PyTorch - The torchrun launcher|link]]) which:
- Starts processes in each pod, one per GPU
- Assigns proper values to environment variables:
	- `RANK`, `LOCAL_RANK`
	- `WORLD_SIZE`
	- `MASTER_ADDR`, `MASTER_PORT`
- Initializes Torch Distributed process group using processes and env vars created earlier
- Runs code from a Ray Trainer API function
# Ray Trainer API function for a long running service
Ray Trainer is designed for batch jobs, so Ray Trainer API function should perform a fixed number of operations, for example load a model and make a single prediction.

It is not recommended but it is also possible to run in that function a long running service like a Rest API endpoint. That endpoint can be created using Ray Serve.

In that case, Ray Trainer starts worker processes which will form a Torch Distributed process group, and one of those processes which loads a model, will also start a Ray Serve actor.

In that case, code would look something like this:
```python
# Function for Ray Trainer API
def inference_worker():
    # 1. init torch distributed / deepspeed
    setup_torch_distributed()
    
    # 2. load model once
    model = load_deepspeed_model()
    
    # 3. start serve actor
    @serve.deployment(route_prefix="/predict")
    class PredictActor:
        def __init__(self, model):
            self.model = model
        def __call__(self, request):
            return self.model(request)
    
    PredictActor.deploy(model)
   
# Ray Trainer API which will start Trainer worker process 
trainer = Trainer(
    train_loop_per_worker=inference_worker, # Training function to use
    backend="torch",  # use PyTorch or "tensorflow", "xgboost", etc.
    num_workers=4,    # number of parallel workers
    use_gpu=True      # whether to use GPU
)
```
# Setting up NCCL communication
DeepSpeed uses NCCL ([[NCCL|link]]) for communication between GPUs. To enable using NCCL in containers on Kubernetes, we can use NVIDIA GPU Operator like described here - [[NVIDIA GPU Operator]].
# Pros and cons
For pros and cons of using Ray Train refer here - [[Ray Train - Pros and cons]].
# Other notes

# Questions
- 