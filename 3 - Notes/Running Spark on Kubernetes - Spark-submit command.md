Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Kubernetes]], [[_Spark]]

# Introduction
To run a Spark script using this option we need to follow those steps:
- Build a Docker image containing our Spark app and script
- Push our Docker image to a could container registry
- Use the spark-submit command in terminal to run that image on the Kubernetes cluster:
![[2 - Images/Spark Running on Kubernetes/Screenshot 1.png]]

Instead of pushing Docker image to a container registry we can use an image saved on each Kubernetes’ node.
# Cons
- Resource cleanup - We need to clean up driver and executor pods after running a job
- Observability
	- We need to get logs from each Driver and Executor Pods
	- Job status difficult to see
	- More difficult to monitor with Prometheus, Grafana, Spark History Server
- Job templating and parametrization
	- It is done through CLI commands
	- More difficult to work with (especially when there is a lot of parameters and they are different for different tasks)
- Retry support
	- We can use Airflow to retry failed jobs
	- It retries the entire job
	- it can’t retry only one Executor Pod
# Pros
- Easier to use