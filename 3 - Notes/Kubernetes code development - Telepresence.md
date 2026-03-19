Tags: [[_Telepresence]]

# Introduction
Telepresence creates a tunnel between our local computer and Kubernetes internal network. 

Thanks to that our computer becomes a part of Kubernetes network, it is like another pod and it can talk to other Kubernetes pods using their service name as DNS name.

It uses an existing kubectl config to connect to Kubernetes.

On windows, it is recommended to use WSL with Ubuntu, edit code in VS code and use the 'remote - WSL' VS code extension. Then we edit code in VS code but files are saved in WSL where Telepresence runs.