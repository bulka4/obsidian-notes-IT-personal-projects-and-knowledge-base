Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
It’s typically a **JSON file** (sometimes YAML is supported) that specifies all the training options, including:
- Optimizer and learning rate schedules
- Mixed precision (FP16/BF16)
- ZeRO settings (stages, offloading ([[DeepSpeed - ZeRO|link]]))
- Tensor and pipeline parallelism ([[DeepSpeed - Tensor and pipeline parallelism|link]])
- Gradient clipping, checkpointing ([[DeepSpeed - Checkpointing|link]]), logging
- Batch sizes, gradient accumulation steps

When we initialize DeepSpeed in code, we pass the path to this file, and the engine reads the settings to configure the training.

That allows to separate the code and hyperparameters, we don’t need to hardcode settings in Python. We can easier experiment with different hyperparameters.

#DistributedComputing #MLEngineering 