Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Pod logs
We can check pod's logs using:
```bash
kubectl -n <namespace> logs <pod-name>
```
# Pod logs live
or we can also watch logs live:
```bash
kubectl -n <namespace> logs -f <pod-name>
```
# Pod events
or we can use the `describe` command ([[Kubernetes - Check pod specification (describe command)|link]]) (which provides pod's specification) and check the events section in the output:
```bash
kubectl -n <namespace> describe <pod-name>
```
# Namespace events
or w can get events for a namespace:
```bash
kubectl get events -n <namespace> --sort-by=.lastTimestamp
```
# Use grep
We can use `grep` ([[Linux & Bash - Grep|link]]) to look for logs containing a specific keyword:
```bash
kubectl -n <namespace> logs <pod-name> | grep keyword
```
# Check logs for a specific container
If our pod runs multiple containers, we can check logs for a specific one using:
```bash
kubectl -n <namespace> logs <pod-name> -c <container-name>
```
# Check status logs in the pod description
We can find logs about a resource in the `status` section in the resource description we can get using this command:
```bash
kubectl get <resource-type> <resource-name> -o yaml
```
