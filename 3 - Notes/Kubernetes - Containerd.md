Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Kubernetes uses containerd as a runtime for running containers. Kubelet is communicating with it.
## Containerd.sock
It is a file which is a Unix domain socket. It is containerd’s endpoint used by clients (like Kubernetes (kubelet) and other CLI tools) for communication with containerd.

Path of that file uniquely identifies that endpoint and is used by clients to connect to containerd (like an IP address).
## Crictl
It is a CLI tool used to interact with container runtimes like containerd.
## Crictl.yaml
It is a configuration file used by the circtl. Amoung the others it specifies a path to the socket (the .sock file) to use.
## Cgroup management – sytemdCgroup configuration
Cgroup is a Linux kernel feature that controls and limits the resource usage (CPU, RAM etc) of groups of processes.

The sytemdCgroup option in the containerd configuration indicates whether or not use systemd for cgroup management.

When sytemdCgroup = true then systemd will be used for cgroup management.

When systemdCgroup = false then containerd will manage cgroups using the cgoupsfs interface independently of systemd.

sytemdCgroup = true is usually required for Kubernetes. It is required if kubelet is using systemd for cgroup management.

#Cloud #DevOps #DistributedComputing #DataEngineering 