Tags: [[_Kubeflow]], [[__Machine_Learning_Engineering]]
#Kubeflow #MLEngineering 

# Introduction
Kubeflow Trainer is a Kubernetes-native project for large language models (LLMs) fine-tuning and enabling scalable, distributed training across a wide range of AI frameworks, including PyTorch, HuggingFace, DeepSpeed, MLX, JAX, XGBoost and others.

With the Kubeflow Python SDK, we can effortlessly develop and fine-tune LLMs while leveraging the Kubeflow Trainer APIs: TrainJob and Training Runtimes.

Kubeflow Trainer fully supports MPI-based ([[MPI (Message Passing Interface)|link]]) distributed training, orchestrating multi-node, multi-GPU jobs efficiently. This ensures high-performance communication between processes, making it ideal for large-scale AI training that requires tight synchronization across GPUs and nodes.

Kubeflow Trainer provides CRDs:
- For running training / inference scripts:
	- TrainJob ([[Kubeflow Trainer - TrainJob CRD|link]])
- For setting up environment where scripts will run:
	- TrainingRuntime ([[Kubeflow Trainer - TrainingRuntime CRD|link]])
	- ClusterTrainingRuntime

Old version of Kubeflow Trainer is Training Operator v1, which provides CRDs:
- MPIJob (deployed with MPI Operator ([[MPI Operator|link]]) which is a part of the the Training Operator v1)
- PyTorchJob (deployed with the Training Operator v1)
# Other notes
MPIJob, TrainingRuntime (and PyTorchJob probably as well) can be used to set up DeepSpeed multi-node cluster on Kubernetes pods and run scripts for training and inference.

Kubeflow Trainer automatically sets up the distributed environment for PyTorch, enabling Distributed Data Parallel (DDP).
# Questions
- What is PyTorch Distributed Data Parallel (DDP)?