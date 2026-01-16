Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes next steps and plan regarding the DeepSpeed cluster project - [[DeepSpeed cluster project|link]].
# Base image
- `nvidia/cuda:XX.Y-cudnn-runtime-ubuntuXX.XX`
# Installed components
- PyTorch (CUDA-compatible)
- DeepSpeed
- Transformers
- Accelerate
- NCCL
# Entry points
Support **two modes**:
1. `inference_server.py` (HTTP or gRPC)
2. `train.py` (future)
# DeepSpeed config JSON
Include DeepSpeed config JSON in the image:
```json
{
  "train_batch_size": 32,
  "gradient_accumulation_steps": 2,
  "fp16": { "enabled": true },
  "zero_optimization": { "stage": 2 }
}
```
