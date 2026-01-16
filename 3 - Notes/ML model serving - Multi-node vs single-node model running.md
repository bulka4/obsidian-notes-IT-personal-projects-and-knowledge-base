Tags: [[__Machine_Learning_Engineering]], [[_ML_model_serving]]
#MLEngineering #MLModelServing

# Introduction
This document describes different aspects of what we can / should take care of when serving ML models.

Serving an ML model is about creating a long-running service (like Rest API server) which listens to requests and sends back model's predictions as a response.

When serving ML models, we have a few options how to run a model:
- On a single node (server) with a single or multiple GPUs
- Multiple nodes
# Multiple nodes
When running a model distributed across many nodes (a single prediction needs to be distributed across many nodes), we usually have only one cluster (set of nodes) running our model.

In that case, all the nodes need to cooperate with each other when performing distributed computations. When one node fails, others can't continue.

We could have another multi-node cluster which can take over in case of failure of the first cluster or when the first cluster is busy, but that approach is rather not used in practice because of complexity and cost.
## Node failure
In a multi-node setup, when one node goes down, the entire system (all the nodes in the cluster) needs to be restarted since that one node holds part of calculation results which are necessary for the final prediction.

Currently, there are no systems for multi-node distributed ML calculations which can survive a single node failure.
## Tools for model serving
For serving a model inference which runs on multiple nodes, we can use tools like:
- Kubeflow TrainingRuntime CRD ([[Kubeflow Trainer - TrainingRuntime CRD|link]])
- Ray Train ([[Ray Train - Introduction|link]])
- MPI Operator ([[MPI Operator|link]])

Those tools are not designed for serving but for batch jobs (where we perform a fixed number of operations and job finishes) but they can efficiently set up a multi-node cluster and restart all the nodes when one node goes down.

For example, they can start on each node proper processes and set up env vars needed to create a Torch Distributed process group ([[Torch Distributed process group|link]]) which is needed to use PyTorch DDP ([[PyTorch - DistributedDataParallel (DDP)|link]]) or DeepSpeed ([[DeepSpeed - Introduction|link]]).

Below are documents describing how to set up a multi-node DeepSpeed cluster using those tools:
- Kubeflow TrainingRuntime CRD ([[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]])
- Ray Train ([[DeepSpeed - Kubernetes deployment with Ray Train|link]])
- MPI Operator ([[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]])
# Single node
When model can be ran on a single node (calculations for a single prediction doesn't have to distributed across many nodes), we can have multiple nodes with an entire model loaded, ready to handle requests (make predictions) independently, without other nodes.
## Node failure
When one node fails, only this one node needs to be restarted, not all the nodes in the cluster, and other nodes can still handle upcoming requests.
## Routing
When we have many nodes, where a single node can handle requests, we can route requests to those nodes which are the least busy.
## Tools
For serving a model inference which runs on a single node, we can use tools like:
- Ray Serve ([[_Ray#Ray Serve|link]])
# Node failures causes and how to avoid them
Node failures are especially costly when our model runs on multiple nodes. In that scenario, as we already mentioned, when one node goes down, the entire system (all the nodes in the cluster) needs to be restarted.

That is costly so we want to avoid such situations.
## OOM (out of memory)
OOM error (out of memory) can make a node to fail. 

To avoid this, we can validate inputs before we process them. Inputs which will require too much computational power can be rejected.