Tags: [[_My_projects]]
#MyProjects 

# Introduction
This document describes next steps and plan regarding the RAG app project - [[RAG app project|link]].
# Additional information
Additional information about next steps and plan:
- [[DeepSpeed - Kubernetes deployment with Ray Serve]]
# Things to take care of
- Autoscaling
- Monitoring
- Handling failures
# Kubernetes setup (Terraform)
Prepare Kubernetes to run Ray Train on GPUs.

More information about that is here - [[RAG app project - Kubernetes setup]]
# Kubeflow TrainingRuntime deployment for DeepSpeed inference
Use Kubeflow TrainingRuntime CRD to deploy a DeepSpeed cluster and Rest API server serving predictions performed using DeepSpeed.

This Rest API will be used to create a new MCP tool which will be used in the LangChain workflow to generate the final answer. 

DeepSpeed cluster is a separate deployment so:
- It is isolated from other parts of the system (mcp server and other Ray Serve deployment serving LangChain workflow) and we can handle failures of different parts separately:
	- We debug and restart only one part instead of all
	- For debugging we investigate logs only from the one part instead of all
- We can scale it separately

More information about it can be found here - [[RAG app project - Kubeflow TrainingRuntime deployment for DeepSpeed inference]]
# Build the DeepSpeed LLM container
Create a dedicated image for using DeepSpeed.

More information about it can be found here - [[RAG app project - DeepSpeed container]]
# Create a new MCP tool
Create a new MCP tool for making predictions with DeepSpeed. It will use Rest API created using Kubeflow TrainingRuntime CRD.

In LangGraph:
- Replace or extend your current LLM node
- The node calls:
    - Internal DeepSpeed LLM service
    - With retrieved documents as context
# Model storage strategy
DeepSpeed startup time is dominated by model loading.
## Option A (simplest, good start)
- Azure Blob Storage
- Download model at pod startup
## Option B (recommended for prod)
- Azure Files or Azure NetApp Files
- Mounted as ReadOnlyMany
- Models cached across restarts
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
# Future extensions and other versions
- Add:
    - LoRA fine-tuning jobs
    - Model registry (MLflow fits nicely here)
- Multi-model routing inside LangGraph
- Cost-aware scheduling (spot GPU pools)
## Single node model inference serving
Instead of running a model for inference distributed across many nodes, take a smaller model and run it on a single node with many GPUs.

Use Ray Serve to create many nodes serving that model where each model handles requests independently (can make predictions on its own).