Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When pod is running, we can save messages in termination logs which will be available in pod's status ([[Kubernetes - Pod status|link]]) once the pod is finished. We can read then those messages using Kubernetes Rest API.
# Add a message to termination logs
In every pod's container there is automatically created the `/dev/termination-log` file where we can save messages, we can just normally edit this file, for example in Python:
```python
import json

result = {"should_retrain": False}

with open("/dev/termination-log", "w") as f:
    f.write(json.dumps(result))
```
or in bash:
```bash
echo "message" > /dev/termination-log
```
# Read messages from termination logs
Once a pod is finished, we can read messages from termination logs which are in pod's status ([[Kubernetes - Pod status|link]]), for example by running:
```python
from kubernetes import client
v1 = client.CoreV1Api()
pod = v1.read_namespaced_pod(pod_name, namespace)
exit_code = pod.status.container_statuses[0].state.terminated.message
```
or
```bash
kubectl get pod $POD_NAME -o jsonpath="{.status.containerStatuses[0].state.terminated.message}"
```