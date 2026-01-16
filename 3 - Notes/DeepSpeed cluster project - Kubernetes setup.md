Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes how to set Kubernetes as a part of the DeepSpeed cluster project - [[DeepSpeed cluster project - Next steps plan]].
# Add GPU node pools
When creating AKS, use:
- NC4as_T4_v3 VMs as nodes (the cheapest with NVIDIA GPU)
- `taints` to avoid non-GPU workloads (on GPU nodes it is better to run only DeepSpeed, without other apps as described here - [[DeepSpeed - Running other apps on the same nodes|link]])
- Enable Azure CNI (already likely done)
	- It gives each pod a real IP from your Azure VNet
# Install GPU prerequisites
## NVIDIA GPU Operator
NVIDIA GPU Operator allows to use CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) by processes running in containers.

It installs on the host:
- libraries:
	- NVIDIA driver ([[NVIDIA Driver|link]])
	- CUDA
	- NCCL
- NVIDIA Container Toolkit ([[NVIDIA Container Toolkit|link]])

NVIDIA Container Toolkit is used by a container runtime (like docker, containerd) to inject (mount) NVIDIA driver ([[NVIDIA Driver|link]]), CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) libraries from the host into the container at runtime, allowing applications to use them in the container.

That allows applications in the container to perform calculations on GPUs.

It also Configures Kubernetes CRI ([[Kubernetes - CRI (Container Runtime Interface)|link]]) to support GPU-enabled containers.

It also adds DCGM exporter which provides GPU metrics for monitoring, such as GPU utilization, memory usage, temperature, power consumption etc.
## `accelerator = nvidia` setting
The `accelerator = nvidia` setting when creating AKS can also be used to enable using CUDA and NCCL but it installs necessary tools on the host which are not automatically available in containers.

We would need to set up NCCL and CUDA in containers additionally.
# Questions
- 