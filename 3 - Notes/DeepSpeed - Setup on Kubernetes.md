Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]
#DeepSpeed #MLEngineering 

# Introduction
Below are tools we can use to set up DeepSpeed ([[DeepSpeed - Setup|link]]) on Kubernetes ([[_Kubernetes|link]]) with links to materials which explain that in more detail:
- MPI Operator ([[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]])
- Kubeflow Trainer - TrainingRuntime CRD - [[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]]
- Ray Train - [[DeepSpeed - Kubernetes deployment with Ray Train|link]]
- Argo / Flyte Workflows
- StatefulSet plus Service

Below table shows a high-level comparison of those tools:

| Tool                     | Starts pods at the same time? | Sets env vars properly? | How well it prepares NCCL      | Prepares an environment to run a single or many jobs? |
| ------------------------ | ----------------------------- | ----------------------- | ------------------------------ | ----------------------------------------------------- |
| MPI Operator             | Yes                           | Yes                     | very good                      | Single                                                |
| TrainingRuntime CRD      | Yes                           | Yes                     | good                           | Single                                                |
| Ray Train                | Yes                           | Yes                     | good                           | Many                                                  |
| StatefulSet plus Service | No                            | No                      | we need to prepare it manually |                                                       |
# StatefulSet plus Service
We do here everything manually. We need to configure pods and communication between them, and run proper commands  make sure that when all the pods are ready
# Other notes
# Questions
- 