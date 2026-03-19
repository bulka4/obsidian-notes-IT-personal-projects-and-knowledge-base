Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
When debugging network on Kubernetes, it is worth to check:
- CoreDNS logs.
- firewall rules using `iptables` ([[Kubernetes - Check firewall rules for kube-proxy and CoreDNS|link]])
- CoreDNS configMap, especially section with the ‘forward’ keyword
- The `resolv.conf` file of a Pod.
- After making changes to CoreDNS restart a coredns deployment:
	```bash
	kubectl rollout restart deployment coredns -n kube-system
	```
- if I can ping from inside of a Pod other Pods / Services using their IP address instead of DNS name