Tags: [[__Machine_Learning_Engineering]]

# Introduction
Ray is a tool for distributed code execution. We can send to Ray code to execute and Ray will choose a node (a computer) from a cluster (set of computers) which has enough resources (CPU, RAM) and will execute this code.

Also different tasks from our code can run simultaneously on different servers.

We have different tools in Ray, for example:
- Ray Core – Basic tool. It is a backbone of other Ray tools.
- Ray Serve – For serving long running Python services that can be accessed via HTTP, gRPC, or directly through Ray APIs.

#MLEngineering 