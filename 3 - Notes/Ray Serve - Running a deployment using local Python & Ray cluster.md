Tags: [[__Machine_Learning_Engineering]]
#MLEngineering 

# Introduction
When we define a deployment, we need to deploy it into a running Ray cluster, for example:
```python
from ray import serve

serve.start() # start SErve (proxy + controller) inside the Ray Cluster

@serve.deployment(route_prefix="/api")
class MyAPI:
	async def __call__(self, request):
		return "Hello world!"
		
# Run the deployment (create actor replicas)
MyAPI.deploy()
```

In this case we need to have a Ray cluster running and run this script on one of the cluster’s nodes.

We can also use the `serve.run()` function which enables creating multiple deployments:
```python
import ray
from ray import serve
from fastapi import FastAPI

app1 = FastAPI()
app2 = FastAPI()

@serve.deployment(route_prefix="/hello")
@serve.ingress(app1)
class Hello:
	async def __call__(self, request):
		return "Hello world!"


@serve.deployment(route_prefix="/goodbye")
@serve.ingress(app2)
class Goodbye:
	async def __call__(self, request):
		return "Goodbye world!"
		
# Bind deployments
hello = Hello.bind()
goodbye = Goodbye.bind()

# Connect to a local or remote cluster
ray.init(address="auto")

# Run all deployments together
serve.run([hello, goodbye])
```
