Tags: [[_Ray]], [[__Machine_Learning_Engineering]]
#Ray #MLEngineering 

# Introduction
Ray Train is Ray’s distributed training layer - it’s a tool that lets us take a regular PyTorch / TensorFlow / XGBoost training code and run it across many CPUs/GPUs and many machines without rewriting the model logic.

Under the hood, Ray Train:
- Starts N training workers (Ray actors)
- Each worker runs the same training function
- Data is **sharded** across workers
- Gradients / metrics are synchronized
- Failures are handled automatically
- Checkpoints are coordinated
# Core components
## Training function
We define a function for training a model:
```python
def train_loop_per_worker():
    model = ...
    optimizer = ...
    for epoch in range(epochs):
        train(...)
        validate(...)
```

This function will be used by a trainer (orchestrator) which will execute that function in a distributed way.
## Trainer (orchestrator)
Ray Train provides Trainers which are used to execute our training function in a distributed way, for example:
```python
from ray.train.torch import TorchTrainer
from ray.train import ScalingConfig

trainer = TorchTrainer(
    train_loop_per_worker=train_loop_per_worker,
    scaling_config=ScalingConfig(
        num_workers=4,
        use_gpu=True
    )
)
result = trainer.fit()
```
What the `Trainer` does:
- Launches Ray actors (workers)
- Allocates CPUs/GPUs
- Sets up communication backends
- Handles retries & restarts
- Aggregates metrics

We never manually create workers.
# What happens at runtime
Let's assume, that we set up:
```python
num_workers = 4
use_gpu = True
```
Below is described what happens next.
## Ray schedules workers
- Ray starts 4 actors
- Each actor gets:
    - 1 GPU
    - Some CPUs
- Actors may live on different nodes
## Distributed backend is initialized
What happens here depends on what framework we use for training a model. If we use for example PyTorch, then:
- Ray initializes torch.distributed
- Chooses a backend (usually NCCL for GPUs)
- Sets:
    - `RANK`
    - `WORLD_SIZE`
    - `MASTER_ADDR`
## Data is sharded
If we use Ray Data:

```python
dataset = ray.data.read_parquet(...) 
trainer = TorchTrainer(     
	train_loop_per_worker,     
	datasets={"train": dataset} 
)
```
Ray:
- Splits dataset into N shards
- Each worker sees only its shard
- Ensures deterministic shuffling

Equivalent to:
> Spark partitioning, but for ML training

Using Ray Data is not required to shard data but it makes it easier.
## Training runs in parallel
Each worker:
- Runs the same training loop
- Processes different data
- Computes gradients locally
## Gradients are synchronized
This depends on the framework:

**PyTorch:**
- Uses DistributedDataParallel (DDP)
- Gradients are:
    - All-reduced
    - Averaged across workers
- Model weights stay identical

**XGBoost / LightGBM:**
- Uses their native distributed logic
- Ray just wires workers together
# Other notes
To create a model by splitting data and performing calculations in parallel on different parts of data, we need to change how calculations are done, how gradients are calculated and parameters updated.

Ray Train does that automatically and it uses for that functionalities of a framework we use, for example if we use PyTorch it uses PyTorch DDP.
# Questions
- 