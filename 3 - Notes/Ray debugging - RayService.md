Tags: [[__Machine_Learning_Engineering]]

# Check logs
## Pod logs
Check Ray head pod logs to see if Ray Serve app has been started:
- `kubectl -n \<namespace> logs \<ray-head-pod>`
## KubeRay operator logs
Use this command to check KubeRay operator logs:
- `kubectl logs -n <namespace> deployment/kuberay-operator`
## Check the `RayService` resource status
Check the `RayService` resource status using this command:
```
kubectl get rayservice <resource-name> -n <namespace> -o yaml
```

For example, we can check there information about the Ray Serve Python application/deployment under the `status` field.
## Exception handler to see Python code error
If we make a Rest API call, it doesn’t work and that is a fault of the Python code handling this request, then in order to see the actual error from the Python code we need to use such an exception handler:
```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse
import traceback
from ray import serve

app = FastAPI()

# Exception handler to see the exact error in Python code when we make a Rest API call and it doesn't work.
@app.exception_handler(Exception)
async def debug_exception_handler(request: Request, exc: Exception):
    return JSONResponse(
        status_code=500,
        content={"error": str(exc), "trace": traceback.format_exc()},
    )
    
@serve.deployment(ray_actor_options={"num_cpus": 2})
@serve.ingress(app)
class RAGService:
```
## Route function logs
To see logs from executing a route function:
```python
@app.get("/search")
    async def ask(self, query: str, top_k: int = 3) -> list:
	    print('log')
```

we can:
- Run a Ray Serve app using the `serve run` command. Then we will see logs in the terminal where we run this command (more convenient).
- Search through the log files when running a Ray Serve app using the `RayService` CRD (less convenient).
### Check logs files in Ray cluster pods
To see logs from executing a route function, we can check files with logs in the `/tmp/ray/session_latest/logs` folder in the Ray cluster pods.

There should be files with logs with name like ‘driver’, ‘serve’ or ‘controller’. They contain info about starting Ray Serve application.

The `python-core-driver-*` logs relates to Serve driver which starts our app.

The `serve/controller-*.log` file can contain info about errors in our Ray Serve app code.

Running processes on Ray head node 

Running `ps aux | grep serve` in the Ray head’s pod should show something like `ray_serve_controller  ... python -m ray.serve ...`
## Check status of applications
Use the following Python function to check the status of an application and logs:
- `import ray; ray.init(); from ray import serve; print(serve.status().applications)`
## Ray dashboard
Port-forward to the head service:
- `kubectl port-forward svc <rayservice-name>-head 8265:8265 -n <namespace>`

And open `http://localhost:8265`. Go to the ‘Jobs’ and ‘Serve’ tabs, there should be visible app and logs.
# Check running jobs / processes
## Ray job CLI
We can use those commands in terminal (run them in Ray head node):
- `ray job list`
- `ray job logs <job-id>`

To find more information about jobs Ray was running.

We can find there for example Serve driver job which starts our Ray Serve app.
## Running processes on Ray head node
Running:
- `ps aux | grep serve`

in the Ray head’s pod should show something like `ray_serve_controller  ... python -m ray.serve ...`
# Tests to do
## Importing a module – `import_path` and `working_dir` configuration
If we have such a configuration in the RayService manifest:
```
serveConfigV2: |
	applications:
		- name: rag-agent-service
		  import_path: "ray_serve_app.rag_agent_service"
		  working_dir: /app
```

Then in the Docker image we are using, we need to be able to run:
```
cp /app
python -c "import ray_serve_app"
```

If that fails, then RayService will not run the Ray Serve app.

RayService is performing such an import of our Ray Serve app.

This can tell us for example if the script ray_serve_app works properly, if there are not any errors.
## Test Rest API
### Using Python
Run this code on the Ray head node in order to make a test Rest API call to our Ray Serve app:
```python
from ray import serve

# Get a handle to the running deployment 
# As deployment-name we specify either the name of the deployment class or RayService CRD name if used.
handle = serve.get_app_handle("deployment-name")
# Make a call using the `ask` endpoint
result = handle.ask.remote(query="Hello")
print(result)
```

Here we make a Rest API call using the ‘ask’ endpoint and the ‘query’ parameter:
```python
app = FastAPI()

@serve.deployment(ray_actor_options={"num_cpus": 2})
@serve.ingress(app)
class RAGService:
    def __init__(...)
    
    @app.get("/ask")
    async def ask (self, query: str):
	    ...
```

This will show us if the Rest API works properly.

If we use ‘curl’ instead, then it might not work due to networking and it might not show us logs about error in the Python code from the API which has occured.
### Using curl
We can also use curl to test our Ray Serve app:
- `curl http://<ray-service-external-ip>:8000/ask?query=Hello`

Where ray-service-external-ip is external IP of a service linked to our Ray head pod and our Ray Serve app is defined like in the example above in the ‘Test Rest API > Using Python’ section.