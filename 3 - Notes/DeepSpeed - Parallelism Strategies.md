Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
DeepSpeed supports multiple kinds of parallelism that can be combined:
- Data parallelism
	- Split data across GPUs
	- Technique for that is ZeRO - [[DeepSpeed - ZeRO|link]]
- Models parallelism - [[DeepSpeed - Tensor and pipeline parallelism|link]]
	- Pipeline parallelism
		- Split computations from multiple neural network layers across GPUs
	- Tensor parallelism
		- Split computations from a single neural network layer across GPUs

#DistributedComputing #MLEngineering 