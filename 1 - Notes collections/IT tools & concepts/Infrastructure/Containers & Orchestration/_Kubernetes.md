Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

This is a collection of documents related to Kubernetes which is an IT tool for managing infrastructure for running software.

# Introduction
1. [[Kubernetes - Introduction]]
2. [[Kubernetes - Benefits]]
# Theory
1. [[Kubernetes - Materials to learn from]]
2. [[Kubernetes - CronJobs]]
3. [[Kubernetes - ConfigMap]]
4. [[Kubernetes - Deployment]]
5. [[Kubernetes - Job]]
6. [[Kubernetes - Kubectl]]
7. Components:
	1. [[Kubernetes - Master node & worker node]]
	2. [[Kubernetes - Components - Container runtime]]
	3. [[Kubernetes - Components - Kubelet]]
	4. [[Kubernetes - Components - Kube proxy]]
	5. [[Kubernetes - Components - API server]]
	6. [[Kubernetes - Components - Scheduler]]
	7. [[Kubernetes - Components - Controller manager]]
	8. [[Kubernetes - Components - Etcd]]
8. [[Kubernetes - Namespace]]
9. [[Kubernetes - Node]]
10. [[Kubernetes - Operators]]
11. [[Kubernetes - Pod]]
	1. [[Kubernetes - Pod metadata]]
	2. [[Kubernetes - Pod containers sharing namespace]]
12. [[Kubernetes - Resources]]
	1. [[Kubernetes - Manifest]]
	2. [[Kubernetes - CRD]]
		1. [[Kubernetes - podTemplateFile]]
13. [[Kubernetes - Replicas]]
14. [[Kubernetes - Service Account]]
	1. [[Kubernetes - Check Service Account permissions]]
15. [[Kubernetes - StatefulSet]]
16. [[Kubernetes - Secret]]
17. [[Kubernetes - Taints]]
18. [[Kubernetes - Volume]]
	1. [[Kubernetes - Persistent Volume (PV)]]
	2. [[Kubernetes - Persistent Volume Claim (PVC)]]
	3. [[Kubernetes - Volume with configMap]]
	4. [[Kubernetes - Dynamic storage provisioner]]
	5. [[Kubernetes - Volume mounting - SubPath]]
	6. [[Kubernetes - PVC access modes]]
	7. [[Kubernetes - Volume mounting -  File permissions]]
	8. [[Kubernetes - Storages for volumes]]
19. [[Kubernetes - Webhooks]]
20. [[Kubernetes - Gang scheduling]]
21. [[Kubernetes - Security Context]]
## Details
1. [[Kubernetes - Containerd]]
2. [[Kubernetes - Kubeconfig file]]
3. [[Kubernetes - Kube context]]
4. [[Kubernetes - CRI (Container Runtime Interface)]]
# Practical notes / good practices
1. [[Kubernetes - Running databases]]
2. [[Kubernetes - Entrypoint as PID 1]]
# Useful commands and tools
1. [[Kubernetes - Port foward]]
2. [[Kubernetes - Checking permissions]]
3. [[Kubernetes - Resources limits and requests]]
4. [[Kubernetes - Checking if pod has enough resources (OOM error)]]
5. Resources in general:
	1. [[Kubernetes - List resources]]
	2. [[Kubernetes - Create, edit and modify resources]]
	3. [[Kubernetes - Get information about a specific resource]]
	4. [[Kubernetes - Check resource status logs]]
	5. [[Kubernetes - Check available fields with descriptions for a specific resource]]
6. Pods
	1. [[Kubernetes - Check pod logs]]
	2. [[Kubernetes - Check pod specification (describe command)]]
	3. [[Kubernetes - Connect to a pod's bash session]]
7. Service
	1. [[Kubernetes - Check pods attached to a service]]
8. Deployment
	1. [[Kubernetes - Restart (rollout) a deployment]]
# Manifest parameters - details
## Pod manifest
1. [[Kubernetes - Pod manifest - Command parameter]]
# Networking
1. [[Kubernetes - Networking]]
2. [[Kubernetes - CNI]]
3. [[Kubernetes - Service]]
4. [[Kubernetes - Ingress]]
5. [[Kubernetes - CoreDNS]]
# Helm
1. [[Kubernetes - Helm]]
2. [[Helm - Helpers]]
3. [[Helm - Pods failures and restarts]]
4. [[Helm - Dependencies]]
5. [[Helm - values.yaml]]
## Helm commands
1. [[Helm - Install dependencies]]
2. [[Helm - Install chart]]
3. [[Helm - Upgrade a chart]]
4. [[Helm - Check rendered YAML manifest that will be applied]]
# AKS
[[AKS - Volumes]]
# Code development on Kubernetes
1. [[Kubernetes - Code development]]
2. [[Kubernetes code development - Telepresence]]
3. [[Kubernetes code development - VS Code and Remote Kubernetes container]]
# Debugging
5. Networking:
	1. [[Kubernetes - Check firewall rules for kube-proxy and CoreDNS]]
	2. [[Kubernetes - Test resolving DNS names]]
	3. [[Kubernetes - Network debugging - Things to check]]
	4. [[Kubernetes - Setting up from scratch - Useful tools for debugging]]
6. Pods:
	1. [[Kubernetes - Create a pod for debugging and get access to its bash session]]
# To learn
1. 