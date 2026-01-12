Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
A kube context is a named entry in the kubeconfig file that tells kubectl which cluster to talk to, as which user, and in which namespace by default.

It contains:
- Cluster – Kubernetes API server endpoint
- User – Auth credentials
- Namespace – Default namespace
- Name – Name of the kube context

All the kube contexts are saved in the Kubeconfig file (~./kube/config).
