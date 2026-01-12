Tags: [[__Machine_Learning_Engineering]]

# Serving a model running on a single node
Ray Serve is a good option, when we want to serve a model inference, where model runs on a single node, i.e. when a single prediction can be done on a single node, it doesn't have to be distributed across many nodes.

In that case, Ray Serve can create many nodes where each node can independently handle requests.
## Features
- When a new request comes in, Ray will route it to the least busy node
- Nodes can be auto-scaled based on a traffic
- When one node fails, only this one node is being restarted and other nodes can take over requests in the meantime
# When not to use Ray Serve
## Training models and serving a model running on multiple nodes
Ray Serve doesn't handle well situations when we want to train or serve a model which runs on multiple nodes, i.e. when a single prediction can't be done on a single node due to a computational cost and it have to be distributed across many nodes.

In that case, all the nodes need to cooperate with each other when performing distributed computations. When one node fails, others can't continue.

Ray Serve is able to set up multiple nodes which will together run a cluster for distributed ML computation, but there will be problems such as:
- We might need to manually set up environment variables on each pod with proper values, what can be complicated to do. Ray Serve doesn't help with that.
- When one node goes down, we need to restart all the nodes in the cluster to make it working again, while Ray Serve will restart only one node

We might encounter such problems, for example when setting up a DeepSpeed cluster like described here - [[DeepSpeed - Kubernetes deployment with Ray Serve]].
# More about model serving
To learn more about serving models running in both a single-node and multi-node setup, refer to this document - [[ML model serving - Multi-node vs single-node model running]].
# Examples
We can use MPI operator, for example to set up a multi-node DeepSpeed cluster like described here - [[DeepSpeed - Kubernetes deployment with Ray Serve]].