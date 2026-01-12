Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Training and serving a model running on multiple nodes
MPI operator is a good option when we want to train or serve a model running on multiple nodes, i.e. when a single prediction needs to be distributed across many nodes due to a computational cost.
# Features
- Can set up a multi-node cluster (start processes on each node and set up env vars)
- When one node in the cluster goes down, it restarts all the nodes in the cluster and reinitiate the cluster so it can work again
# When not to use MPI operator
## Training a model running on a single node
If the model can run on a single node, then MPI operator is not needed.
## Serving a model running on a single node
If we want to serve a model which can run on a single node, then MPI operator is not a good option.

In that scenario, we would like to:
- Create multiple nodes, where each node can independently handle requests
- When one node fails, we restart only that one node
- Auto-scale nodes based on a traffic
what can't be achieved with MPI operator. 

MPI operator would restart all the nodes when a single node fails and can't auto-scale.

For that purpose, it is better to use for example Ray Serve.
# More about model serving
To learn more about serving models running in both a single-node and multi-node setup, refer to this document - [[ML model serving - Multi-node vs single-node model running]].
# Examples
We can use MPI operator, for example to set up a multi-node DeepSpeed cluster like described here - [[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)]].