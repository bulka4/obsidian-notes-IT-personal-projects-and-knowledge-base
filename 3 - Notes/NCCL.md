Tags: [[_Communication_frameworks]]
#CommunicationFrameworks 

# Introduction
NCCL (NVIDIA Collective Communications Library) is a GPU-optimized communication library enabling data exchange between processes running on GPUs, both within a single computer and across multiple computers.

It’s commonly used in distributed deep learning to coordinate tensors across multiple GPUs.

It is mainly used to perform collective operations such as:
- `all-reduce` → combine values from all GPUs and distribute the result
- `broadcast` → send data from one GPU to all others
- `reduce` → combine data to a single GPU
- `all-gather` → collect data from all GPUs

Key features:
- GPU-focused: Maximizes bandwidth and latency performance on NVIDIA GPUs.
- Multi-node support: Works across multiple machines connected via high-speed interconnects.
- Seamless integration: Used by PyTorch (`torch.distributed`), TensorFlow, Horovod, and DeepSpeed.