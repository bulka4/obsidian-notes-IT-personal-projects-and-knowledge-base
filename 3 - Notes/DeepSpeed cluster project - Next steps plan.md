Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes next steps plan regarding the DeepSpeed cluster project - [[DeepSpeed cluster project|link]].
# Kubernetes setup (Terraform)
Prepare Kubernetes nodes to run DeepSpeed on GPUs.

More information about that is here - [[DeepSpeed cluster project - Kubernetes setup]]
# Kubeflow TrainingRuntime deployment for DeepSpeed inference
Use Kubeflow TrainingRuntime CRD to deploy a DeepSpeed cluster and Rest API server serving predictions performed using DeepSpeed.

More information about it can be found here - [[DeepSpeed cluster project - Kubeflow TrainingRuntime deployment for DeepSpeed inference]]
# Build the DeepSpeed LLM container
Create a dedicated image for using DeepSpeed.

More information about it can be found here - [[DeepSpeed cluster project - DeepSpeed container]].
# Model storage strategy
DeepSpeed startup time is dominated by model loading.
## Option A (simplest, good start)
- Azure Blob Storage
- Download model at pod startup
## Option B (recommended for prod)
- Azure Files or Azure NetApp Files
- Mounted as ReadOnlyMany
- Models cached across restarts
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
# Future extensions and other versions
- Add:
    - LoRA fine-tuning jobs
    - Model registry (MLflow fits nicely here)
- Cost-aware scheduling (spot GPU pools)