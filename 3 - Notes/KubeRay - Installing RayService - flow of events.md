Tags: [[__Machine_Learning_Engineering]]

# Introduction
Here are the steps followed to install RayService CRD:
- RayService CRD (YAML) is applied
- KubeRay operator submits a Ray Job to the head node
	- That job is called Serve driver. It runs in its own pod or in the head pod. It is a Python process that imports our file with Ray Serve app and runs the bound deployment.
	- Import_path parameter from the RayService CRD is used by the KubeRay and Serve driver.
	- For example if our RayService has this configuration:
```
serviceConfigV2: |
	applications:
		name: rag-agent-service
		import_path: "ray_serve_app:rag_agent_service"
```

And our Ray Serve app looks like this:
```
@serve.deployment
@serve.ingress(app)
class RAGAgentService:
	...
	
rag_agent_service = RAGAgentService.bind()
```

Then Serve driver will run internally something like:
```
import ray_serve_app
app = ray_serve_app.rag_agent_service
serve.run(app)
```
- Serve driver connects to the Ray cluster, launches the ServeController, and registers our deployment(s).
- Once the Serve driver is running, we will see logs like ray_serve_controller.out under /tmp/ray/session_latest/logs/.

#MLEngineering 