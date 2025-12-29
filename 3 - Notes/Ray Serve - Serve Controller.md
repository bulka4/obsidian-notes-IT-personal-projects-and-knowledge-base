Tags: [[__Machine_Learning_Engineering]]

# Introduction
Serve Controller manages the state and lifecycle of deployments. Here is described what it does:
1. **Deployment management**
	- Keeps track of deployments we have defined (names, configs, resources).
	- Creates/destroys replicas (actors) according to your configuration or autoscaling.
	- Ensures deployments are healthy (restarts replicas if they crash).
2. **Configuration & API**
	- Exposes the management API (serve.run, serve.deploy, etc.).
3. **Routing metadata**
	- Maintains routing metadata which is used by the Serve Proxy to decide which replica should handle a request

#MLEngineering 