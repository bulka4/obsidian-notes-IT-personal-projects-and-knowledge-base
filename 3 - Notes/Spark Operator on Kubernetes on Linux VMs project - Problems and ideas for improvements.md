Tags: [[_My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Kubernetes resources deployment
It might be a good idea to change the bash script for configuring VM1, vm1_configure.tftpl, such that it only configures Kubernetes but doesn't deploy any resources.

That script can create another bash script and save it on the VM1, which will contain code for deploying all the Kubernetes resources. It can be executed manually after creating VMs and configuring Kubernetes cluster.

Maybe creating resources too early causes some problems.

Although if we do this, then Spark Operator pods (controller and webhook) will be deployed on the worker node and then deploying SparkApplication CR doesn't work (it is described in more detail in the 'Spark Operator Webhook' section below).

Deploying Kubernetes resources manually after Kubernetes cluster is set up might be good idea but first we would need to solve the problem from the 'Spark Operator Webhook' section.
# Volume with Spark scripts
Because volume with Spark scripts used by Spark Driver and Executors' Pods' is linked into the node which is running those Pods, that means that we need to have that script on all the cluster nodes (because Pods can be deployed on any node).

If we create a new script using Jupyter Notebook, it will be saved only on one node, the one running Jupyter (VM1). We would need to copy it to the second VM in order to be able to run it on Kubernetes.

There are two options for improving it:
- Save Spark scripts in the Docker image - Then we don't need to use volume mounts at all but we need to push updated image into the ACR every time we have a new script.
- Save Spark scripts in shared storage - For example in the MinIO running on the same Kubernetes cluster or in cloud object storage.
# Spark Operator Webhook
We have the following problems:
- When spark operator pods (controller and webhook) are created on the worker node, then:
    - When we try to deploy the SparkApplication in the default namespace, then we get an error about the webhook: 'failed to call webhook ... context deadline exceeded'.
    - When we try to deploy the SparkApplication in the spark-operator namespace (the same as spark operator pods), then it gets deployed but nothing happens (it doesn't change status, there are no logs, Spark Driver Pod doesn't get created)
- When spark operator pods are created on the master node, then we can deploy the SparkApplication resource and it gets completed.
    - In order to be able to deploy spark operator pods on the mater node, we need to patch their deployments and add tolerations (it is done in the bash script vm1_configure.tftpl)

The issue from the next section 'DNS resolution' is related to this.

Forums about similar issues:
- [https://stackoverflow.com/questions/72059332/how-can-i-fix-failed-calling-webhook-webhook-cert-manager-io](https://stackoverflow.com/questions/72059332/how-can-i-fix-failed-calling-webhook-webhook-cert-manager-io)
- [https://stackoverflow.com/questions/74783557/metallb-kubernetes-installation-failed-calling-webhook-ipaddresspoolvalidation](https://stackoverflow.com/questions/74783557/metallb-kubernetes-installation-failed-calling-webhook-ipaddresspoolvalidation)
# DNS resolution
There is a problem with resolution of public and Services DNS names from inside of a Pod. This is related to the issue from the previous section 'Spark Operator Webhook'.

Symptoms:

- At the beginning, after cluster setup, we can't resolve public and Services DNS names from inside of a Pod. When we restart the coreDNS deployment `kubectl -n kube-system rollout restart deployment coredns`, it starts working, but deploying SparkApplication still gives the same error about the webhook.
# Terraform code sometimes doesn't work
Sometimes not entire bash script is executed successfully on one of the VMs and we need to run the entire Terraform code again (I don't know why).