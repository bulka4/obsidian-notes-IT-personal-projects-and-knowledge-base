Tags: [[__Machine_Learning_Engineering]]

# RayService
## Pod logs
Check Ray head pod logs to see if Ray Serve app has been started:
- kubectl -n \<namespace> logs \<ray-head-pod>
## KubeRay operator logs
Use this command to check KubeRay operator logs:
- kubectl logs -n \<namespace> deployment/kuberay-operator
## Check RayService resource status
Check the RayService resource status using this command:
- kubectl get rayservices.ray.io \<resource-name> -n \<namespace> -o yaml

And look under the ‘status’ field.
## Check logs files in Ray cluster pods
In the Ray cluster pods we can check files with logs in the /tmp/ray/session_latest/logs folder.

There should be files with logs with name like ‘driver’, ‘serve’ or ‘controller’. They contain info about starting Ray Serve application.

The ‘python-core-driver-*’ logs relates to Serve driver which starts our app.

The serve/controller-*.log file can contain info about errors in our Ray Serve app code.

Running processes on Ray head node 

Running ‘ps aux | grep serve’ in the Ray head’s pod should show something like ‘ray_serve_controller  ... python -m ray.serve ...’
## Check status of applications

Use the following Python function to check the status of an application and logs:
- import ray; ray.init(); from ray import serve; print(serve.status().applications)
## Ray job CLI
We can use those commands in terminal (run them in Ray head node):
- ray job list
- ray job logs \<job-id>

To find more information about jobs Ray was running.

We can find there for example Serve driver job which starts our Ray Serve app.
## Ray dashboard
Port-forward to the head service:
- kubectl port-forward svc/\<rayservice-name>-head 8265:8265 -n \<namespace>

And open [http://localhost:8265](http://localhost:8265). Go to the ‘Jobs’ and ‘Serve’ tabs, there should be visible app and logs.
## Running processes on Ray head node
Running:
- ps aux | grep serve

in the Ray head’s pod should show something like ‘ray_serve_controller  ... python -m ray.serve ...’
## Importing a module – import_path and working_dir configuration
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
![[2 - Images/Ray - Debugging/Screenshot 1.png]]

Here we make a Rest API call using the ‘ask’ endpoint and the ‘query’ parameter:
![[2 - Images/Ray - Debugging/Screenshot 2.png]] 

This will show us if the Rest API works properly.

If we use ‘curl’ instead, then it might not work due to networking and it might not show us logs about error in the Python code from the API which has occured.
### Using curl
We can also use curl to test our Ray Serve app:
- curl http://\<ray-service-external-ip>:8000/ask?query=Hello

Where ray-service-external-ip is external IP of a service linked to our Ray head pod and our Ray Serve app is defined like in the example above in the ‘Test Rest API > Using Python’ section.
## Exception handler to see Python code error
If we make a Rest API call, it doesn’t work and that is a fault of the Python code handling this request, then in order to see the actual error from the Python code we need to use such an exception handler:
![[2 - Images/Ray - Debugging/Screenshot 3.png]]