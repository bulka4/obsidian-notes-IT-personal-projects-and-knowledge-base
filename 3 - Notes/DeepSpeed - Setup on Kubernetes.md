Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
We can set up a DeepSpeed ([[DeepSpeed - Setup|link]]) cluster for two purposes:
- Batch job - Running a fixed amount of tasks and script finishes
- Inference serving - A service that runs all the time, listens to requests from other applications and sends predictions as responses, like Rest API

Below are tools we can use to set up DeepSpeed on Kubernetes ([[_Kubernetes|link]]) for both purposes with links to materials which explain that in more detail:
- Inference serving:
	- Ray Serve - [[DeepSpeed - Kubernetes deployment with Ray Serve|link]]
- Both batch job and Inference serving:
	- StatefulSet plus Service
	- MPI Operator - [[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]]
	- Kubeflow Trainer - TrainingRuntime CRD - [[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]]
	- Ray Train - [[DeepSpeed - Kubernetes deployment with Ray Train|link]]
- Others (not explored yet)
	- Argo / Flyte Workflows
# Easiness of use and flexibility
Some of those tools are easier to use but offers less flexibility. Below are assigned scores for each tool where:
- Score 1 means the most difficult to use and the most flexibility
- Score 5 means the least difficult to use and the least flexibility

Tools scores:
- StatefulSet plus Service - 1
- MPI Operator - 2
- Kubeflow Trainer - TrainingRuntime CRD - 3
- Ray Train - 5
- Ray Serve:
	- For serving a model which can run on a single node - 5
	- For serving a model which needs to be distributed across many nodes (a single prediction needs to be distributed) - 2 (it is not designed for such a scenario)
# Setting up NCCL communication
DeepSpeed uses NCCL ([[NCCL|link]]) for communication between GPUs. To enable using NCCL in containers on Kubernetes, we can use NVIDIA GPU Operator like described here - [[NVIDIA GPU Operator]].
# StatefulSet plus Service
We do here everything manually. We need to configure pods and communication between them, run proper commands, make sure that all the pods are ready when we start initializing DeepSpeed cluster.
# Other notes
# Questions
- 