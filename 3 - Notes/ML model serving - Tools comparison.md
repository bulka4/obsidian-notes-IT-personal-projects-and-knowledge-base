Tags: [[__Machine_Learning_Engineering]]

# Introduction
This document describes and compares different tools for building Rest APIs which are efficient for serving ML models ([[ML model serving - Introduction|link]]).
# Tools comparison
## Ray Serve
More info about Ray Serve - [[_Ray#Ray Serve|link]].

**Pros:**
- Load balancing
	- When Rest API server receives multiple requests, Ray Serve can distribute those requests across multiple servers
- Request’s tasks distribution
	- When a single Rest API call consists of multiple tasks, Ray Serve can distribute those tasks across multiple servers and run them in parallel.
	- For example, when a request consist of tasks like:
		- Two different models makes predictions (2 tasks)
		- Make additional calculation using those predictions
	  
	  then Ray Serve can assign different tasks to different nodes.
- Task level fault tolerance
	- If one Rest API call consist of multiple tasks, each of them can be executed independently, at the same time, potentially on different servers.
	- If one task fails is can be retried without affecting other tasks and restarting the entire Rest API call
- Request batching
	- When server receives multiple requests, Ray Serve can combine them into a single forward pass.
	- For example it can take data from multiple requests and run a single process where ML model makes predictions using it.
	- This is more efficient when making predictions using GPUs.
- Autoscaling
	- Ray Serve can automatically increase or decrease number of replicas of our app depending on a traffic (number of requests coming in).
- Source aware scheduling
	- When we create an app, we can specify how much resources (CPU, GPU) we want to have available for it.
	- When Ray will be creating processes which will be executing our code, it will run them on nodes which have enough of those resources.
- Fractional GPUs
	- We can assign a fraction of a GPU for our app. So Ray Serve makes it easier to run multiple processes on a single GPU.
	- For example in Kubernetes we need to allocate the entire GPU for one Pod (we can’t run multiple Pods on the same GPU).
	- If we want to run multiple processes at the same time using the same GPU even without using Kubernetes or containers at all, then using Ray Serve it might be easier as well.
- Flexible resource allocation
	- When we create an app and assign resources to it like explained earlier in the 'Source aware scheduling' point, we can split our app into multiple parts (each part will be handling different endpoints) and to each part we can assign different resources
- Python native and flexible
	- We can easily deploy any Python code along with the model.
	- Good when we want to serve as Rest API multi step, complex code.

**Cons:**
- Ray Serve makes it easier to create an efficient distributed Rest API by abstracting away from us a lot of difficulties in setting it up but that abstraction makes debugging harder. It is harder to find out what is happening and why.
## KServe
**Introduction:**
KServe is good for creating Rest APIs on Kubernetes which:
- Serves a single ML model prediction
- Chains multiple ML models in such a way, that output of one model is used as an input for another model.

But it is not good if we want to create more complex workflows, for example:
- Make prediction with one model
- Retrieve data from a database
- Make some calculations (other than model predictions)
- Make another prediction with another model

**Pros:**
- Rest API endpoints out of the box
	- Clients can make calls and we don’t need to write our own API code
- Autoscaling
	- Automatically scales up/down Pods based on traffic
	- Uses Knative-based autoscaling which is very reliable in Kubernetes-native environments
- Supports multiple ML frameworks
	- TensorFlow, PyTorch, ONNX, XGBoost, Hugging Face
- InferenceGraph support
	- Allows chaining multiple models/workflow steps
- Kubernetes native
	- It is built using almost only Kubernetes tools

**Cons:**
- Complex workflows implementation
	- Complex workflows which we want to serve as Rest API, for example Python scripts performing multiple tasks, not only makes a single prediction, are more difficult to implement
- Request batching is not native
	- It can be obtained using for example Triton integration.
## BentoML
**Type:** Python-native ML model serving framework.

**Key Features:**
- Packaged ML models as REST/gRPC endpoints.
- Model versioning and reproducibility.
- Docker containerization automatically.
- Supports multiple frameworks (PyTorch, TensorFlow, XGBoost, Hugging Face).

**Pros:**
- Easy to deploy models as APIs.
- Good for packaging ML pipelines.
- Can integrate with Kubernetes, AWS Lambda, or SageMaker.

**Cons:**
- Less suited for **multi-step distributed workflows** inside a single request.
- Request batching is limited.

**Usage workflow:**
- Package your model using **BentoML’s Python API** (BentoService or newer bentoml.Model + bentoml.Service).
- Define **REST/gRPC API endpoints** inside the BentoML service.
- Containerize automatically using bentoml containerize.
- Deploy on **Kubernetes**, AWS, or other cloud platforms using the generated container.

**Example usage:**
```python
import bentoml
from bentoml.io import JSON

@bentoml.artifacts([PickleArtifact("model")])
@bentoml.env(auto_pip_dependencies=True)
class MyService(bentoml.BentoService):
	@bentoml.api(input=JSON(), output=JSON())
	def predict(self, parsed_json):
		return self.artifacts.model.predict(parsed_json["input"])
```
## TensorFlow Serving
**Type:** Model server specialized for TensorFlow.

**Key Features:**
- High-performance serving of TF SavedModels.
- Supports versioned models and hot-swapping.
- gRPC and REST endpoints.

**Pros:**
- Optimized for TensorFlow models; high throughput.
- Supports batching efficiently.

**Cons:**
- TensorFlow-only.
- Hard to integrate arbitrary Python code or multi-step pipelines.

**Usage workflow:**
- Export your TensorFlow model as a SavedModel.
- Start TFServing server pointing to the SavedModel directory.
- Access via REST or gRPC endpoint.
- Deploy on Kubernetes as a Deployment + Service, optionally with autoscaling.

**Example usage:**
```
tensorflow_model_server \
	--rest_api_port=8051 \
	--model_name=my_model \
	--model_base_path=/models/my_model
```
## TorchServe
**Type:** Model server specialized for PyTorch.

**Key Features:**
- Serve PyTorch models via REST/gRPC.
- Multi-model, multi-version support.
- Request batching, logging, metrics.

**Pros:**
- Optimized for PyTorch, good performance.
- Easy to deploy PyTorch pipelines.

**Cons:**
- PyTorch-only.
- Limited flexibility for custom Python workflows or multi-step task orchestration.

**Usage workflow:**
- Export your PyTorch model as a .mar archive using **Torch Model Archiver**.
- Start TorchServe server pointing to the model store.
- Access via **REST/gRPC endpoints**.
- Deploy on Kubernetes using Deployment + Service.

**Example usage:**
```
torch-model-archiver \
	--model-name my_model \
	--version 1.0 \
	--serialized-file model.pt \
	--handler handler.py
	
torchserve \
	--start \
	--ncs \
	--model-store model_store \
	--model my_model.mar
```
## Triton Inference Server
**Type:** Multi-framework high-performance inference server.

**Key Features:**
- Supports TensorFlow, PyTorch, ONNX, TensorRT, Hugging Face.
- Batching, concurrent model execution.
- GPU and multi-GPU optimization.

**Pros:**
- Very high throughput for large models.
- Supports multiple frameworks in the same server.
- Can serve models with mixed precision and GPU optimization.

**Cons:**
- Harder to integrate arbitrary Python code inside pipeline.
- More complex to set up for non-standard workflows.

**Usage workflow:**
- Export your model in a **supported format** (TensorFlow SavedModel, PyTorch TorchScript, ONNX, TensorRT).
- Organize models in a **model repository folder**, one folder per model.
- Start Triton Server pointing to the repository.
- Access models via **REST or gRPC API**.
- Deploy on Kubernetes using Deployment + Service.

**Example usage:**
```
tritonserver --model-repository=/models --http-port=8000 --grpc-port=8001
```
## Amazon SageMaker
**Type:** Fully managed ML model serving.

**Key Features:**
- Deploy models from any supported framework.
- Autoscaling, monitoring, versioning.
- Supports multi-model endpoints and A/B testing.

**Pros:**
- Fully managed; minimal ops.
- Integration with AWS ecosystem.

**Cons:**
- Less flexible for custom multi-step Python workflows.
- Vendor lock-in; cost can scale with usage.

**Usage workflow:**
- Train or import your model (supports many frameworks).
- Create a **model in SageMaker** pointing to S3 location of model artifacts.
- Deploy model as **endpoint** using SageMaker SDK or console.
- SageMaker automatically handles REST API creation, scaling, and monitoring.

**Example usage:**
```python
import sagemaker
from sagemaker.pytorch import PyTorchModel

model = PyTorchModel(
	model_data = "s3://bucket/model.tar.gz"
	,role=role
	,entry_point="inference.py"
)

predictor = model.deploy(instance_type="ml.m5.large", initial_instance_count=1)
```
## Azure Machine Learning Endpoints
**Type:** Fully managed ML model serving.

**Key Features:**
- REST endpoints for models.
- Autoscaling and model versioning.
- Supports multiple frameworks.

**Pros:**
- Managed service, easy Kubernetes deployment under the hood.
- Good integration with Azure ecosystem.

**Cons:**
- Less flexible for custom Python workflows and task-level parallelism.
- Limited low-level control over deployment and request routing.

**Usage workflow:**
- Register your model in Azure ML workspace.
- Create a **Python scoring script** (defines REST API) and an environment (conda/pip dependencies).
- Deploy as **Managed Online Endpoint**.
- Azure handles scaling, REST endpoint exposure, and logging.

**Example usage:**
```python
from azure.ai.ml import MLClient
from azure.ai.ml.entities import ManagedOnlineEndpoint, ManagedOnlineDeployment

endpoint = ManagedOnlineEndpoint(name="my-endpoint")
deployment = ManagedOnlineDeployment(
	name="blue"
	,endpoint_name="my-endpoint"
	,model=model
	,code_configuration=code_config
)
ml_client.begin_create_or_update(endpoint)
ml_client.begin_create_or_update(deployment)
```
## Summary table

| Tool       | Python flexibility | Multi-step Workflows | Multi-framework       | Autoscaling | GPU routing | Request Batching |
| ---------- | ------------------ | -------------------- | --------------------- | ----------- | ----------- | ---------------- |
| Ray Serve  | High               | High                 | Yes (any Python code) | Yes         | Yes         | Yes              |
| BentoML    | High               | Medium               | Yes                   | Yes         | Partial     | Limited          |
| TFServing  | Low                | Low                  | TF only               | Limited     | Partial     | Yes              |
| TorchServe | Low                | Low                  | PyTorch only          | Limited     | Partial     | Yes              |
| Triton     | Low                | Low                  | Multi                 | Limited     | Yes         | Yes              |
| SageMaker  | Medium             | Medium               | Multi                 | Yes         | Yes         | Limited          |
| Azure ML   | Medium             | Medium               | Multi                 | Yes         | Yes         | Limited          |
# Comparison of Ray Serve to a load balancer
Load balancer takes care of assuring that each server receives a similar amount of requests.

It doesn’t look at the computational cost of those requests. So different servers might receive the same amount of requests, but total amount of computational resources required for those requests might be much bigger for some of those servers.

Load balancer distributes only the entire requests, that is it chooses a server which will handle the entire request.

In contrast, Ray Serve can split multiple tasks from a single request across multiple servers and it is aware of computational resources of those servers.
# Request batching explanation
Request batching is beneficial because when making model’s predictions for a single input doesn’t utilize the entire GPU, then we make predictions for a few inputs at the same time utilizing the entire GPU.

When performing predictions for a single input doesn’t fit on a single GPU, then it is still beneficial because of a few factors explained below.

**Specific calculations are more efficient**
Some parts of calculations might not be utilizing the entire GPU (for example a single matrix multiplication).

**Communication between GPUs is more efficient**
When different GPUs performs different calculations, they need to share with each other their results.

When each GPU performs more calculations (for more inputs), then instead of sharing results for each input separately, they share them all at once which is faster.

**Pros and cons**
With this approach we have the following pros and cons:
- Latency goes up – Because still each GPU can run longer
- Throughput goes up – Total tokens / sec goes up and it goes up much higher than latency