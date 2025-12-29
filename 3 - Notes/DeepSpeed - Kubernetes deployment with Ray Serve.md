Tags: [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[__Machine_Learning_Engineering]]

# Introduction
Ray Serve can be used to set up a DeepSpeed cluster and create a Rest API endpoint which will serve model's predictions done by DeepSpeed.

When we deploy a RayService CRD, it creates Pods which will run DeepSpeed processes ([[DeepSpeed - Torch Distributed processes|link]]).

When setting up a DeepSpeed cluster using Ray Serve, there are problems with:
- Creating all the Pods at the same time
- Creating environment variables on each Pod with proper values (like RANK, MASTER_ADDR)

It looks like this is quite complicated and not good option for doing this, it is better to use MPI operator ([[DeepSpeed - Kubernetes deployment with MPI Operator (MPIJob CRD)|link]]), Ray Train ([[DeepSpeed - Kubernetes deployment with Ray Train|link]]) or Kubeflow Trainer TrainingRuntime CRD ([[DeepSpeed - Kubernetes deployment with Kubeflow Trainer (TrainingRuntime CRD)|link]]) which solves problem Ray Serve has.
# Setting up a DeepSpeed cluster guide
Here is described how to set up DeepSpeed cluster using RayService CRD:
1. Creating Pods
	- RaySercice creates Pods (replicas) on which DeepSpeed workers will run.
	- We specify number of Pods to create with the num_replicas variable in the Ray Serve deployment.
	- We need to use Ray placement groups to make sure that all the Pods are started at the same time. Otherwise, if some of the workers are ready and others are still pending, or workers are ready or master is pending, DeepSpeed init will fail.
2. AKS resources - We need to create:
	- StatefulSet for the DeepSpeed Master and Ray Serve app – guarantes a stable DNS name for the Master Pod
	- RayService – which will create Pods (replicas) which will act as Workers
	- Use the Master’s DNS name as the MASTER_ADDR env variable in every Pod
	- Create Master before RayService – so the Worker nodes can connect to the Master
	
	Every Pod will have automatically:
	- Proper hostname resolution
	- Open network ports for MASTER_PORT
	- Enabled TCP communication to other Pods
1. Code setup
	- Create two scripts:
		- Deepspeed_init.py
			- Initializes DeepSpeed (runs a Worker)
		- Langgraph_workflow.py
			- Initializes DeepSpeed (runs a Master)
			- Runs Rest API which serves LangGraph workflow, which answers questions using DeepSpeed.
	- Langgraph_workflow.py code runs on Master Pod, created by the StatefulSet
	- Deepspeed_init.py code runs on the Worker Pods, i.e. replicas created by the RayService
2. Environment Variables - Create the following env variables on each node:
	- MASTER_ADDR → IP of the master pod.
	- MASTER_PORT → port used for NCCL communication.
	- RANK → Global rank of this worker. Unique across all processes.
	- WORLD_SIZE → total number of GPUs across all nodes.

	How to create them:
	- We can use Ray Serve to create those env variables on each Pod.
	- Choosing a value for the RANK:
		- RANK = replica index
			- Index of a Pod’s replica created by RayService. We can get that value in Python code using ray.serve.get_replica_context().replica_tag
		- If there are multiple GPUs per Pod, then RANK = GPU index
	
	Why those variables are needed:
	- Using those variables all the nodes tries to connect to the Master and this way Master knows which Pods belong to the cluster.
4. Expose GPUs to Pods
	- Install NVIDIA Device Plugin so the Pods can use GPUs:
	
	kubectl apply -f [https://raw.githubusercontent.com/NVIDIA/k8s-device-plugin/v0.14.0/nvidia-device-plugin.yml](https://raw.githubusercontent.com/NVIDIA/k8s-device-plugin/v0.14.0/nvidia-device-plugin.yml)