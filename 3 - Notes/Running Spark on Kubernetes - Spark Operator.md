Tags: [[__Data_Engineering]], [[__Distributed_computing]], [[_Kubernetes]], [[_Spark]]

# Introduction
## Created resources
### Deployments
Spark Operator is running its own Deployments called ‘spark-operator-xxxx’. One is spark operator controller and second is spark operator webhook (if using webhook).
### Pods
There are Pods running for each Deployment.
### Services
Spark Operator is running its own Services called ‘spark-operator-xxxx’.
### Service Accounts
Spark Operator’s Pods are using Service Accounts which need to have proper permissions. We can check what are those Accounts by checking configurations of Pods:

Kubectl get pod \<pod-name> -n \<namespace> -o yaml
## Webhooks
Spark Operator uses webhooks to talk to a Kubernetes API server in order to modify resources. They are using certificates for security. Certificates files are mounted into a webhook Pod.

We can check how certificates are mounted it by checking webhook Pod specification:
- kubectl get pod -n \<namespace> \<webhook-pod-name> -o yaml

Webhooks allows us to provide some additional fields for Driver and Executors Pods specification, which are not supported by the SparkApplication. For example adding tolerations.

We can also use PodTemplateFile to add additional specification fields.
## Taints and tolerations
In order to run Spark Operator on a master node (control plane) we need to set up proper tolerations for spark-operator-controller and spark-operator-webhook (if webhook is enabled) deployments.

We can run Spark Operator normally on worker nodes, without setting up tolerations.

We need to patch and restart deployments for both spark-operator-controller and spark-operator-webhook:


#DataEngineering #DistributedComputing #Kubernetes #Spark 