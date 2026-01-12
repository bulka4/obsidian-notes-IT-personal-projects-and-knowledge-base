Tags: [[_Ray]], [[__Machine_Learning_Engineering]]
#Ray #MLEngineering 

# Introduction
Ray Train API is a high-level interface in Ray Train that orchestrates distributed training. It handles:
- Launching multiple workers (processes / actors ([[Ray Core - Actors|link]]))
- Splitting data across workers
- Aggregating gradients and synchronizing model parameters
- Checkpointing and logging

Ray Train API performs batch jobs, that is:
- Loads a model
- Performs predictions (one or many, but fixed amount)

It is not designed to run a service which listens to requests and performs predictions for every request.
# Components
## Training function
A function that:
- Is called by default 'train_loop_per_worker' 
- Defines calculations we want to perform
- Runs once per worker
- Receives `train_dataset` (sharded automatically), `model`, `optimizer`, etc.
## Trainer class

```python
from ray.train import Trainer

trainer = Trainer(
    train_loop_per_worker=train_loop_per_worker, # Training function to use
    backend="torch",  # use PyTorch or "tensorflow", "xgboost", etc.
    num_workers=4,    # number of parallel workers
    use_gpu=True      # whether to use GPU
)
```
The backed which we choose here (PyTorch, TensorFlow etc.) will be responsible for distributed calculations, i.e. splitting data, aggregating gradients and synchronizing parameters.

If our training function is called train_loop_per_worker, then it will be used by default.

For example, in case of PyTorch, that function will handle creating a Torch Distributed process group ([[Torch Distributed process group|link]]).
## ScalingConfig
Defines resources per worker: CPUs, GPUs, etc. 

It can be used in the Trainer class, for example:
```python
from ray.train import ScalingConfig
from ray.train import Trainer

scaling_config = ScalingConfig(
    num_workers=4,
    use_gpu=True
)

trainer = Trainer(
    train_loop_per_worker=train_loop_per_worker, # Training function to use
    backend="torch",  # use PyTorch or "tensorflow", "xgboost", etc.
    scaling_config=scaling_config
)
```
## Dataset
- Can be Ray Data, Torch Dataset, TensorFlow Dataset, or plain Python objects
- `Trainer` shards the dataset automatically across workers
## Running
```python
trainer.start() # Initialize workers
results = trainer.run(train_loop_per_worker) # Execute the training function
trainer.shutdown() # Clean up resources
```
## Cleaning resources
The `trainer.shutdown()` function cleans up resources such as:
- Worker processes / actors
- Objects in the Ray object store created during training
- Closes inter-worker communication channels used for gradient synchronization or parameter updates.

It frees memory and compute.
## Checkpointing
We can save model state during training and resume training later from the checkpoint. It saves:
- Model parameters
- Optimizer states (like in Adam [[Adam optimizer|link]])
- Gradients

Saving checkpoint:
```python
from ray.train import Checkpoint

def train_loop_per_worker(config):
    model = config["model"]
    optimizer = config["optimizer"]
    
    for epoch in range(config["epochs"]):
        # training code ...
        
        # save checkpoint
        checkpoint = Checkpoint.from_dict({
            "model_state_dict": model.state_dict(),
            "optimizer_state_dict": optimizer.state_dict()
        })
        # Trainer automatically handles saving to storage if needed

trainer.run()
checkpoint = trainer.save_checkpoint()
```

Resuming training from a checkpoint:
```python
from ray.train.torch import TorchTrainer

trainer = TorchTrainer(
    train_loop_per_worker=train_loop_per_worker,
    scaling_config={"num_workers": 4},
)

trainer.start()
trainer.load_checkpoint(checkpoint)  # restore previous model state
trainer.run(train_loop_per_worker)
```
# Questions
- 