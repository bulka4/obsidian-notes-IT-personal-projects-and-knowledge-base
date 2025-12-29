Tags: [[_DeepSpeed]], [[__Machine_Learning_Engineering]]
#DeepSpeed #MLEngineering 

# Introduction
DeepSpeed MII (Model Inference Interface) is a Python library for inference of deep learning models (making predictions). 

It automatically applies a lot of optimizations under the hood so we don't need to do this on our own and write a lot of code.
# Deployment
To deploy a server which will expose gRPC endpoint and listen to requests, we use mii.deploy() function:
```
import mii

mii.deploy(
    model_name="facebook/opt-6.7b",
    deployment_name="opt67b",
    num_gpus=2
)
```
We can use here models from HuggingFace.

It starts PyTorch distributed processes and DeepSpeed inference engine.

As a request we send an input for a model and as a response we get model's prediction.

All the created processes runs locally, only on the server where we run mii.deploy().
# Inference
Once we deployed a gRPC endpoint, we can use it for inference.

To send a request we use the mii.pipeline() function:
```
pipe = mii.pipeline(
	deployment_name="opt67b"
	,host=host_name
	,port=port_number
)

pipe("What is ZeRO inference?")
```
where host and port are for the server running the deployed gRPC endpoint.

When creating a pipeline, we specify what kind of tasks we want to do, for example:
- Convert text into embeddings
- Classify text
- Provide answer to a question
- Generate an image based on text
# Multi node set up
MII can't be used to run inference distributed across many servers (distributing a single model's prediction across servers).

All the processes started by mii.deploy() function, which will run the inference, run locally, only on the server where we run this command.
# Benefits
## Optimizations used
DeepSpeed MII uses:
- Fused kernels ([[DeepSpeed - Kernel fusion|link]])
- Tensor parallelism ([[DeepSpeed - Tensor and pipeline parallelism|link]])
- Quantization ([[DeepSpeed - Quantization|link]])
- ZeRO ([[DeepSpeed - ZeRO|link]])
## Serving system
MII gives us:
- Request batching and queue
- Optional token streaming
- Warm model startup
- Predictable latency under sustained load
## Little code needed
It can be run with little code as shown earlier in sections 'Deployment' and 'Inference'.
## High throughput for inference
MII is optimized for many concurrent requests:
- Smart batching
- Efficient KV cache
- Good GPU utilization