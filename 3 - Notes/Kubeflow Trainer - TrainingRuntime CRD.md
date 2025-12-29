Tags: [[_Kubeflow]], [[__Machine_Learning_Engineering]]
#Kubeflow #MLEngineering 

# Introduction
TrainingRuntime is a CRD ([[Kubernetes - CRD|link]]) provided by Kubeflow Trainer ([[Kubeflow Trainer - Introduction|link]]). It is a runtime ([[Runtime|link]]), i.e. set of instructions / configuration, which define how to start and execute code from the TrainJob CRD ([[Kubeflow Trainer - TrainJob CRD|link]]) (which perform calculations related to machine learning (training or inference)).

It defines:
- How pods are created
- How processes are launched
- How to set up environment variables (like`MASTER_ADDR`, `WORLD_SIZE`, `RANK`)
- Networking, restart behavior
- Which command to use to launch processes (torchrun ([[PyTorch - The torchrun launcher|link]]), deepspeed, mpirun ([[MPI - The mpirun command|link]]) etc.)
- Failure policy

Trainer controller manager will execute instructions from the TrainingRuntime CRD.
# Other notes

# Questions
- 