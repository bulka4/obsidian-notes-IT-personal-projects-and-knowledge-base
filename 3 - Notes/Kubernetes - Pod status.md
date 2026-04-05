Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When a pod runs and after it is finished, we can read information from its status, for example about:
- Exit code (from the process running in the pod)
- Termination logs ([[Kubernetes - Termination logs (write a message which can be read from pod's status)|link]])

We can read this info using for example:
- Python
  ```python
	from kubernetes import client
	v1 = client.CoreV1Api()
	pod = v1.read_namespaced_pod(pod_name, namespace)
	exit_code = pod.status.container_statuses[0].state.terminated
  ```
- bash
  ```bash
	kubectl get pod $POD_NAME -o jsonpath="{.status.containerStatuses[0].state.terminated}"
  ```