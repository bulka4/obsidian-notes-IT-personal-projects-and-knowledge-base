Tags: [[__Data_Engineering]] [[_Airflow]]
#DataEngineering #Airflow 

# Introduction
If we run an Airflow task which starts a new Kubernetes pod (e.g. using `KubernetesPodOperator`), then we might want to get some information about this task and:
- Use it for next, downstream Airflow tasks
- Decide whether or not to progress with next, downstream Airflow tasks using `ShortCircuitOperator` ([[Airflow - Conditional tasks in a DAG|link]])

For example, we might want to read data from a database about a performance of a ML model (and we do this in a new pod because connecting to that database requires to prepare an environment properly) and using that data we decide whether or not to progress with next tasks for training a new ML model.

There are a few options to do this, described below.
# Exit code
Code running in the pod can exit with a specific exit code, for example:
```python
import sys
<your-code>
sys.exit(10)
```
Then we can read this exit code in Airflow DAG from pod's status ([[Kubernetes - Pod status|link]]) and take some action based on it:
```python
from kubernetes import client
v1 = client.CoreV1Api()
pod = v1.read_namespaced_pod(pod_name, namespace)
exit_code = pod.status.container_statuses[0].state.terminated.exit_code
```
# Pod termination message
Inside the pod's container, we can write pod termination logs ([[Kubernetes - Termination logs (write a message which can be read from pod's status)|link]]):
```python
with open("/dev/termination-log", "w") as f:
    f.write("SKIP_RETRAIN=true")
```
Then, in Airflow DAG we can read those logs from pod's status:
```python
from kubernetes import client
v1 = client.CoreV1Api()
pod = v1.read_namespaced_pod(pod_name, namespace)
message = pod.status.container_statuses[0].state.terminated.message
```
# XCom
If we use `KubernetesPodOperator`, it is also possible to use XCom to pass information to further tasks as explained here - [[Airflow - Using XCom when running a task starting a Kubernetes pod]].

But it doesn't work if we start a pod using a custom code, like `kubernetes.client` library.
# Applications
Below sections describe how we can use an output from a pod started in a task.
## Conditional DAG tasks
For example, we can use information from the pod running an Airflow task to decide whether or not to progress with next, downstream tasks using `ShortCircuitOperator` ([[Airflow - Conditional tasks in a DAG|link]]).
