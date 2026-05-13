Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]] [[_Kubernetes]]
#Cloud #DevOps #DistributedComputing #DataEngineering #Kubernetes 

# Interacting with AKS from a local computer
We can use kubectl to interact with AKS from our local computer.

We need to follow those steps:
- Install Azure CLI
- Login to Azure using Azure CLI: az login
- Get AKS Credentials
	- We need to merge the AKS credentials into our local kubeconfig so kubectl can connect to our cluster. For doing this we use this command:
		- `az aks get-credentials --resource-group <your-resource-group> --name <your-aks-cluster-name>`

If we don’t have it yet, we can install kubectl using this command:
- `az aks install-cli`
# SSH into AKS
We can connect from our computer to worker nodes in our AKS cluster through SSH.

We can’t connect to the control plane. This one is fully manged by Microsoft.

We get a shell with full access to a worker node (a Linux VM). Using it we can for example fo the following things:
- Modify its filesystem
- Install packages
- Inspect running processes
- Run any bash script