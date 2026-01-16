Tags: [[__Machine_Learning_Engineering]]
#MLEngineering 

# Introduction
Deployment is an object used for running a long-running service, for example a Rest API server.

We typically create a deployment by creating a Python class decorated with `@serve.deployment`. Its methods can for example specify how to handle HTTP endpoints:
```python
from ray import serve
from fastapi import FastAPI

# create FastAPI app
app = FastAPI()

@serve.deployment(route_prefix="/api")
@serve.ingress(app)
class MyAPI:
	def __init__(self):
		pass
		
	@app.get("/hello")
	async def hello(self, name: str = "world"):
		return {"message": f"Hello, {name}!"}
		
# Bind the deployment
my_api = MyAPI.bind()
```

Deployment is a logical definition of a service. 
# Running a deployment
After running a deployment, Ray Serve creates:
- One or more replicas ([[Ray Serve - Replica|link]]) which are processes which will be executing deployment's code
- Proxy ([[Ray Serve - Serve Proxy|link]]) that listens to clients' requests and forwards them to a proper replica that will handle it (execute deployment's code) and send back a response

Replicas are ran on a Ray cluster ([[Ray - Cluster|link]]), each replica can be ran on a different node in the cluster.

We can assign to a deployment specific amount of resources (CPU, GPU) which are needed. Ray will ran each replica on a node which have enough of those resources.