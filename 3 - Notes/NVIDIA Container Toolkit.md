Tags: [[_Hardware_abstraction]]
#HardwareAbstraction

# Introduction
NVIDIA Container Toolkit is used by a container runtime (like docker, containerd) to inject (mount) NVIDIA driver ([[NVIDIA Driver|link]]), CUDA ([[CUDA|link]]) and NCCL ([[NCCL|link]]) libraries from the host into the container at runtime, allowing applications to use them in the container.

That allows applications in the container to perform calculations on GPUs.