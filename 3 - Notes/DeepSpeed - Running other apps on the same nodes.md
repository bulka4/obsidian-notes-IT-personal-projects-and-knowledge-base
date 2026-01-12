Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]], [[_DeepSpeed]]
#DistributedComputing #InfrastructureEngineering #MLEngineering #DeepSpeed 

# Introduction
Running other applications on the same servers as DeepSpeed is not a good idea because other apps can have spikes where they:
- Consume a lot of CPU and RAM - Then DeepSpeed needs to wait for those resources to be available again
- Increase network traffic - Then DeepSpeed communication is slowed down
  
DeepSpeed (and distributed ML computations on GPUs in general) works best if:
- CPU and RAM availability is stable
- Networking is predictable (messages takes always a similar amount of time to arrive)

DeepSpeed uses GPUs for calculations and:
- CPU is needed for GPU calculations, for example for launching GPU kernels ([[GPU kernel and threads|link]])
- RAM is used by CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) which are used to perform calculations on GPUs

When DeepSpeed performs calculations distributed across many nodes, then those nodes need to communicate with each other, for example to perform collective operations ([[DeepSpeed - Collective operations|link]]), so network performance is important here.
# Questions
- 