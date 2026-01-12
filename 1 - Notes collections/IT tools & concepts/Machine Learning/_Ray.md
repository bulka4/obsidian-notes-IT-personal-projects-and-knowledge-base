This is a collection of documents related to Ray, an IT tool for ML model training, inference and serving.

# Debugging
1. [[Ray debugging]]
# Deployment on Kubernetes
1. [[Ray - Deployment on Kubernetes using KubeRay]]
	1. [[KubeRay - RayService]]
		1. [[KubeRay - RayService - YAML configuration]]
		2. [[KubeRay - Installing RayService - flow of events]]
# Introduction
1. [[Ray - Introduction]]
# How Ray works
1. [[Ray - Cluster]]
	1. [[Ray - Head node]]
	2. [[Ray - Worker nodes]]
2. [[Ray - Processes]]
	1. [[Ray - Raylet]]
	2. [[Ray - Worker processes]]
	3. [[Ray - Plasma object storage]]
		1. [[Ray - Serialization]]
	4. [[Ray - GCS (Global Control Store)]]
	5. [[Ray - Dashboard]]
# Ray Serve
1. [[Ray Serve - Introduction]]
## How it works
1. [[Ray Serve - Components]]
	1. [[Ray Serve - Deployment]]
	2. [[Ray Serve - Replica]]
	3. [[Ray Serve - Serve Proxy]]
	4. [[Ray Serve - Serve Controller]]
2. [[Ray Serve - Multiple replicas for one actor]]
3. [[Ray Serve - Multiple deployments]]
4. [[Ray Serve - Running a Deployment]]
	1. [[Ray Serve - Local Python & Ray cluster]]
	2. [[Ray Serve - Kubernetes RayService CRD]]
5. [[Ray Serve + FastAPI - HTTP requests handling workflow and communication]]
6. [[Ray Serve - Python functions for monitoring]]
7. [[Ray Serve - Checkpoints]]
## Use cases and features
1. [[Ray Serve - Use cases and features]]
## Features, pros and cons
[[ML model serving - Tools comparison]]
# Ray Core
1. [[Ray Core - Actors]]
	1. [[Ray Core Actors - Asynchronous methods call]]
	2. [[Ray Core Actors - Processes communication and workflow]]
2. [[Ray Core - Tasks]]
	1. [[Ray Core Tasks - Asynchronous task call]]
	2. [[Ray Core Tasks - distributed and parallel execution]]
	3. [[Ray Core Tasks - Processes communication and workflow]]
# Ray Train
1. [[Ray Train - Introduction]]
2. [[Ray Train - Pros and cons]]
3. [[Ray Train - API]]
4. [[Ray Train - Use cases and features]]
# Ray Data
1. [[Ray Data - Introduction]]

# Topics to learn next
## 1. Trainer lifecycle & execution details
**Why:** helps debug weird behavior and resource leaks
- Trainer vs Driver vs Workers
- When workers are created / reused / destroyed
- What runs on **rank 0 only** vs all workers
- `run_config`, `failure_config`, retries
## 2. Advanced checkpointing patterns
**Why:** critical for long-running jobs
- Checkpoint frequency & best-checkpoint selection
- Partial checkpoints (model-only vs full state)
- Resuming training from checkpoints
- Checkpoints on:
    - Local FS
    - NFS
    - Object storage (S3 / GCS / Azure Blob)
## 3. Metrics & reporting internals
**Why:** avoid silent failures and bad metrics
- `train.report()` vs framework logging
- Aggregation across workers
- Step/epoch semantics
- Integration with MLflow / TensorBoard
## 4. Distributed data at scale (beyond basics)
**Why:** data is often the bottleneck
- Ray Data execution model (blocks, pipelines)
- Streaming datasets vs materialized datasets
- Windowed / iterable datasets
- Dataset → Torch / TF conversion details
- Data locality & prefetch tuning
## 5. Performance tuning
**Why:** default ≠ optimal
- Batch size scaling rules
- Gradient accumulation vs more workers
- NCCL / Gloo backend choice
- CPU vs GPU worker ratios
- Object store memory tuning
- Avoiding serialization overhead
## 6. Fault tolerance & recovery
**Why:** this is where Ray shines vs raw DDP
- Worker failure vs node failure
- Restart semantics
- Elastic training (changing worker count)
- What _cannot_ be recovered automatically
## 7. Inference & non-training workloads
**Why:** Ray Train is useful beyond training
- Distributed batch inference
- Offline scoring jobs
- Feature computation using trained models
- When to use:
    - Ray Train
    - Ray Data
    - Ray Core actors
## 8. Integration with Ray Tune
**Why:** hyperparameter tuning is the natural next step
- Train + Tune relationship
- Trial-level parallelism vs worker-level parallelism
- Resource packing strategies
- Checkpoint handoff between Train and Tune
## 9. Kubernetes & cloud deployments
**Why:** production reality
- Ray Train on K8s (RayCluster CRD)
- GPU scheduling & node affinity
- Autoscaling behavior
- Spot/preemptible nodes
- Persistent volumes for checkpoints
## 10. When _not_ to use Ray Train
**Why:** good engineers know tradeoffs
- Single-GPU training
- Extremely tight latency inference
- Pure data processing (Spark might win)
- Very large model parallelism (DeepSpeed, Megatron)