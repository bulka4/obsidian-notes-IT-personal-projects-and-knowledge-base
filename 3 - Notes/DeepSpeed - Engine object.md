Tags: [[__Distributed_computing]], [[__Machine_Learning_Engineering]]

# Introduction
Engine is a logical object created in our code which is used to interact with DeepSpeed. It is used to start calculations and get results.

When we create an engine, we create one copy per GPU (per Master / Worker process ([[DeepSpeed - Torch Distributed processes|link]])).

It uses a PyTorch model and optimizer which we created, and is responsible for coordinating calculations between GPUs - gets data from other GPUs and sends data to other GPUs when needed for calculations.

#DistributedComputing #MLEngineering 