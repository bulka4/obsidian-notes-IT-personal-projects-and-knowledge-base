Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
DeepSpeed runs one process per GPU. Those processes are launched by Torch Distributed ([[Torch Distributed|link]]).

DeepSpeed additionally uses the process with rank 0 as a master for:
- Ensuring every process knows which part of tensors it owns and uses for calculations (when those tensors are partitioned across GPUs using ZeRO partitioning ([[DeepSpeed - ZeRO|link]]))
- Logging, monitoring, orchestrating checkpointing ([[DeepSpeed - Checkpointing|link]])

#DistributedComputing #MLEngineering 