This is a collection of notes related to DeepSpeed, an IT tool for distributed ML model computing (training and inference).

# Setup
1. [[DeepSpeed - Setup]]
# Kubernetes deployment
1. [[DeepSpeed - Setup on Kubernetes]]
2. [[DeepSpeed - Kubernetes deployment with Ray Serve]]
3. [[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)]]
4. [[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)]]
5. [[DeepSpeed - Kubernetes deployment with Ray Train]]
# Inference
1. [[DeepSpeed - MII]]
# How it works
1. [[DeepSpeed - Introduction]]
2. [[DeepSpeed - Materials to learn from]]
3. [[DeepSpeed - Role of CPU, RAM and GPU]]
4. [[DeepSpeed - Communication between GPUs]]
	1. [[DeepSpeed - NCCL]]
5. [[DeepSpeed - Torch Distributed processes]]
6. [[DeepSpeed - Engine object]]
7. [[DeepSpeed - TCP]]
8. [[DeepSpeed - CUDA]]
9. [[DeepSpeed - Quantization]]
10. [[DeepSpeed - Kernel fusion]]
11. [[DeepSpeed - Configuration files]]
12. [[DeepSpeed - Checkpointing]]
13. [[DeepSpeed - Activation checkpointing]]
## Distributed computations
1. [[DeepSpeed - Parallelism Strategies]]
	1. [[DeepSpeed - ZeRO]]
	2. [[DeepSpeed - Tensor and pipeline parallelism]]
2. [[DeepSpeed - Collective operations]]
## Transformer calculations optimization
1. Attention layer:
	1. [[DeepSpeed - KV caching]]
	2. [[DeepSpeed - Blockwise KV Storage (Paged KV-cache)]]
	3. [[DeepSpeed - Rolling KV caching]]
	4. [[DeepSpeed - MQA and GQA]]
	5. [[DeepSpeed - Chunked (Blockwise) Attention]]
	6. [[DeepSpeed - Sliding Window Attention]]
	7. [[DeepSpeed - Flash Attention]]
2. Others
	1. [[DeepSpeed - Prefill - decode optimization]]
	2. [[DeepSpeed - Continuous (dynamic) batching]]
## Calculation stability
1. [[DeepSpeed - Training stability tools]]
	1. [[DeepSpeed - Numerical stability]]
	2. [[DeepSpeed - Distributed-training stability]]
# How to use it
## Writing code
1. [[DeepSpeed - Running a script (deepspeed command)]]
2. [[DeepSpeed - Initializing a model]]
## Preparing nodes
1. [[DeepSpeed - Running other apps on the same nodes]]
# Computer hardware
When learning about DeepSpeed, it is also good to learn about hardware (especially GPUs):
1. [[_Computer_hardware]]
2. [[_Hardware_abstraction]]
# Concepts to learn
1. 