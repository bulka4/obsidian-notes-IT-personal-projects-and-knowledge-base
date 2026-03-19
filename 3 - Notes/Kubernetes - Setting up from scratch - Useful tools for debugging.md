Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Here are useful tools for debugging when setting up Kubernetes from scratch:
- `crictl ps -a` – list the running and stopped containers.
- `Crictl logs <containerID>` - check logs for a given container
- `ss -tuln | grep 6443` – check processes listening on the 6443 port
- `ps aux | grep kube-apiserver` – check processes in which the ‘kube-apiserver’ string appears.
- `journalctl -u kubelet -f`– view logs from the kubelet process
- `kubectl get pods -n kube-system` – Check pods in the kube-system namespace
- `telnet 10.0.1.4 6443` – try to connect over TCP to the server with the 10.0.1.4 IP address over the 6443 port.