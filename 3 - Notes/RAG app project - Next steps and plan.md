Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes next steps and plan regarding the RAG app project - [[RAG app project|link]].
# Additional information
Additional information about next steps and plan:
- [[DeepSpeed on K8s with MPI - Guide from ChatGPT]]
- [[DeepSpeed - Kubernetes deployment with Ray Serve]]
# Things to take care of
- Autoscaling
- Monitoring
- Handling failures
- 
# AKS and infrastructure changes (Terraform)
## Add GPU node pools
- Add dedicated GPU node pools to AKS:
	- Use NC-series or ND-series VMs
- Key settings:
	- `accelerator = nvidia
	- `taints` to avoid non-GPU workloads
	- Enable **Azure CNI** (already likely done)
## Install GPU & MPI prerequisites via Helm
Install the following cluster-wide components:
1. NVIDIA GPU Operator
    - Drivers
    - CUDA
    - NCCL
    - DCGM (metrics)
2. MPI Operator
    - Enables `MPIJob` CRDs
    - Handles launcher + worker pods

**Questions:**
- 
# Model storage strategy
DeepSpeed startup time is dominated by model loading.
## Option A (simplest, good start)
- Azure Blob Storage
- Download model at pod startup
## Option B (recommended for prod)
- Azure Files or Azure NetApp Files
- Mounted as ReadOnlyMany
- Models cached across restarts
# Build the DeepSpeed LLM container
Create a dedicated image for using DeepSpeed.
### Base image
- `nvidia/cuda:XX.Y-cudnn-runtime-ubuntuXX.XX`
### Installed components
- PyTorch (CUDA-compatible)
- DeepSpeed
- Transformers
- Accelerate
- MPI (OpenMPI or Intel MPI)
- NCCL
### Entry points
Support **two modes**:
1. `inference_server.py` (HTTP or gRPC)
2. `train.py` (future)
# MPIJob for DeepSpeed inference
MPI Operator gives us:
- Handling multi-node coordination
- Correct NCCL environment
- Simple scaling (`replicas`)

MPIJob structure:
- Launcher pod - Runs DeepSpeed launch
- Worker pods
    - Each has 1+ GPUs
    - Uses `hostNetwork: true` (often required for NCCL)

Exposing the service:
- Launcher runs a model server
- Expose via ClusterIP Service
- LangGraph calls it via HTTP
# LLM server API design
Design a **thin, OpenAI-compatible-ish API**:
`POST /v1/chat/completions POST /v1/completions`
Why?
- Easy LangGraph integration
- You can later swap:
    - DeepSpeed
    - vLLM
    - TGI
    - External APIs

Your FastAPI RAG service should treat this as **just another tool**.
# Integrate with LangGraph & MCP
Create a new MCP tool for making predictions with DeepSpeed.

In LangGraph:
- Replace or extend your current LLM node
- The node calls:
    - Internal DeepSpeed LLM service
    - With retrieved documents as context
# Scheduling & resource isolation
Kubernetes:
- GPU node pool taints
- Pod tolerations
- Resource limits:
    `nvidia.com/gpu: 1`
    
Ray:
- Keep Ray Serve **CPU-only
- Do NOT schedule Ray workers on GPU nodes

This avoids resource contention.
# Observability & debugging
Metrics (with Prometheus and Grafana)
- GPU utilization (DCGM)
- Inference latency
- Tokens/sec

Logs
- NCCL debug logs
- DeepSpeed logs
- MPI logs

Health checks
- `/healthz` on LLM server
- Kubernetes readiness probes
# Security & networking
- Internal-only Service (ClusterIP)
- No public exposure of LLM pods
- Optional:
    - NetworkPolicies
    - mTLS between services
# Future extensions
- Swap MPI + DeepSpeed with:
    - DeepSpeed-MII
    - vLLM (for inference-heavy workloads)
- Add:
    - LoRA fine-tuning jobs
    - Model registry (MLflow fits nicely here)
- Multi-model routing inside LangGraph
- Cost-aware scheduling (spot GPU pools)
# DeepSpeed setup
How to set up DeepSpeed is described here - [[DeepSpeed - Setup]].