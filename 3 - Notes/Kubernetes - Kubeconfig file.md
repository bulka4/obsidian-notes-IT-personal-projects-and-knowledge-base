Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
The Kubernetes config file (Kubeconfig file) contains configuration files that kubectl uses to connect and authenticate to Kubernetes and it is located usually at /etc/kubernetes/admin.conf.

When Linux user uses kubectl, then those configuration files specifies which Kubernetes user will be used for executing kubectl commands, like creating resources.

Depending on which configuration files are used, user might see different resources in Kubernetes because of permissions assigned to the Kubernetes user which is used.

We use the KUBECONFIG environment variable to specify which Kubeconfig file will be used by the current Linux user. More info in the ‘KUBECONFIG environment’ section.

Some kubectl or helm commands might fail silently if we are using wrong Kubeconfig file.
## KUBECONFIG variable
This environment variable indicates a path to the Kubernetes configuration file (admin.conf) which will be used by the current Linux user.

If it is not set up then Kubernetes will look for that config file in the default location ~/.kube/config.

#Cloud #DevOps #DistributedComputing #DataEngineering 