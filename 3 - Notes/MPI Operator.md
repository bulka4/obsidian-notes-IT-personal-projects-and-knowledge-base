Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
MPI Operator is a Kubernetes operator ([[_Kubernetes|link]]), which is a part of Kubeflow Trainer ([[Kubeflow Trainer - Introduction|link]]), for running MPI jobs ([[MPI job|link]]) on Kubernetes. It can create and configure pods to enable communication using MPI ([[MPI (Message Passing Interface)|link]]) and other communication frameworks like NCCL ([[NCCL|link]]).

MPI Operator handles:
- Job scheduling (decide which process to run on which node and CPU / GPU)
- Pod creation
- Networking (ensuring communication between pods is configured for MPI or other frameworks)

MPI jobs are created using the MPIJob CRD ([[Kubernetes - CRD|link]]). Once MPIJob CRD is deployed, the MPI Operator creates:
- Launcher Pod - Which starts the MPI job, coordinates workers and runs the mpirun command ([[MPI - The mpirun command|link]])
- Worker Pods - Which run computation tasks

Key features:
- Multi-node support: Can run across multiple nodes for distributed workloads.
- Fault-tolerant: Can restart failed pods (depending on settings).
- Resource management: Integrates with Kubernetes resource limits/requests.

Advantages:
- Avoids manual management of MPI across nodes.
- Kubernetes handles scaling, scheduling, and network setup.
- Integrates seamlessly with Kubeflow pipelines or other K8s workloads
# Other notes

# Questions
- 
