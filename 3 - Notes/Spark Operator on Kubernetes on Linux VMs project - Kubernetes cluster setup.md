Tags: [[__My_projects]] [[__Data_Engineering]]
#MyProjects #DataEngineering 

# Introduction
Kubernetes is configured using bash scripts ran by Terraform ([[Spark Operator on Kubernetes on Linux VMs project - VMs configuration|link]]) which:
- Installs:
	- `containerd`
	- `kubeadm`, `kubelet`, and `kubectl`
- Uses Calico as the Container Network Interface (CNI).
- Creates a join command that can be used to join other servers to the Kubernetes cluster