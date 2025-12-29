Tags: [[__DevOps]], [[__Infrastructure_Engineering]], [[_Docker]] 

# Introduction
Docker uses containerd as a runtime for running containers. Docker is communicating with it.

Alternative is the dockerd.
### Containerd.sock
It is a file which is a Unix domain socket. It is containerd’s endpoint used by clients (like Kubernetes (kubelet) and other CLI tools) for communication with containerd.

Path of that file uniquely identifies that endpoint and is used by clients to connect to containerd (like an IP address).
### Crictl
It is a CLI tool used to interact with container runtimes like containerd.
### Crictl.yaml
It is a configuration file used by the circtl. Amoung the others it specifies a path to the socket (the .sock file) to use.

#DevOps #InfrastructureEngineering #Docker 