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
# Prepare a DeepSpeed cluster
Prepare a multi-node DeepSpeed cluster with a Rest API server serving distributed inference using that cluster. That is a separate project described here - [[DeepSpeed cluster project]].

This Rest API will be used to create a new MCP tool which will be used in the LangChain workflow to generate the final answer.

DeepSpeed cluster is a separate deployment so:
- It is isolated from other parts of the system (mcp server and other Ray Serve deployment serving LangChain workflow) and we can handle failures of different parts separately:
	- We debug and restart only one part instead of all
	- For debugging we investigate logs only from the one part instead of all
- We can scale it separately

DeepSpeed will run on its own dedicated nodes where other apps will not run. Why it is a good practice, is described here - [[DeepSpeed - Running other apps on the same nodes]].
# Create a new MCP tool
Create a new MCP tool for making predictions with DeepSpeed. It will use Rest API created using Kubeflow TrainingRuntime CRD.

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
# Security & networking
- Internal-only Service (ClusterIP)
- No public exposure of LLM pods
- Optional:
    - NetworkPolicies
    - mTLS between services
# Future extensions and other versions
- Multi-model routing inside LangGraph
## Single node model inference serving
Instead of running a model for inference distributed across many nodes, take a smaller model and run it on a single node with many GPUs.

Use Ray Serve to create many nodes serving that model where each model handles requests independently (can make predictions on its own).