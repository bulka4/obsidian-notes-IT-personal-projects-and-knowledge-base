Tags: [[_Kubeflow]], [[__Machine_Learning_Engineering]]
#Kubeflow #MLEngineering 

# Introduction
TrainJob is a CRD ([[Kubernetes - CRD|link]]) provided by Kubeflow Trainer ([[Kubeflow Trainer - Introduction|link]]). It is used to run scripts which perform calculations related to machine learning (training or inference).

In TrainJob we define:
- Container image
	- It must contain code we want to run and ML tools (frameworks) we want to use, like PyTorch, DeepSpeed, CUDA, NCCL.
- Command to run the code
- Number of nodes and GPUs to use
- Runtime reference

To deploy TrainJob CRD, i.e. to execute code from it on a Kubernetes cluster, we need to specify that in the TrainingRuntime CRD ([[Kubeflow Trainer - TrainingRuntime CRD|link]]).