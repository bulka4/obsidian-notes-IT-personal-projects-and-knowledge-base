Tags: [[_Hardware_abstraction]]
#HardwareAbstraction

# Introduction
NVIDIA GPU Operator allows to use CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) by processes running in containers.

It installs on the host:
- libraries:
	- NVIDIA driver ([[NVIDIA Driver|link]])
	- CUDA
	- NCCL
- NVIDIA Container Toolkit ([[NVIDIA Container Toolkit|link]])
- NVIDIA Device plugin (exposes GPUs to Kubetneres so pods can request, be scheduled on and access GPUs)

NVIDIA Container Toolkit is used by a container runtime (like docker, containerd) to inject (mount) NVIDIA driver ([[NVIDIA Driver|link]]), CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) libraries from the host into the container at runtime, allowing applications to use them in the container.

That allows applications in the container to perform calculations on GPUs.

It also Configures Kubernetes CRI ([[Kubernetes - CRI (Container Runtime Interface)|link]]) to support GPU-enabled containers.

It also adds DCGM exporter which provides GPU metrics for monitoring, such as GPU utilization, memory usage, temperature, power consumption etc.
# Questions
- 