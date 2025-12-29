Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
Checkpointing is a process of saving to disk:
- Model progress during training so training can resume after a break 
- Saving model itself so it can be used later for inference

Checkpointing saves:
- Model weights
- Optimizer state (like in Adam ([[Adam optimizer|link]]))
- Training progress (step number, epoch)

#DistributedComputing #MLEngineering 