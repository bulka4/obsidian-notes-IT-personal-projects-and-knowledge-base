Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
It is a DNS server. It translates domain (DNS) names into IP addresses inside of a cluster. That means that once we assign a DNS name to a Pod then every other Pod from a cluster can resolve it.

Every Pod get assigned a default DNS name like this:
- \<pod-ip-address\>.\<namespace\>.pod.cluster.local

We can also use a Service resource in order to assign a static IP address and our chosen domain name to a Pod. Then everytime we recreate that Pod it will have always the same domain name.
## Kube-dns
Kube-dns is CoreDNS’ Service.

Pods should have in the /etc/resolv.conf file a Cluster IP of the kube-dns (or coreds) Service so they can use the kube-dns for resolving DNS names of other Pods / Services.

In CoreDNS logs we can see some information about the traffic.

The iptables is used to control traffic inside the cluster, including communication to the DNS server. We can use it to see for example the firewall rules.
## CoreDNS configMap
In the CoreDNS configMap, next to the ‘forward’ keyword, there is specified an IP address of the DNS server which will be used for resolving DNS names which CoreDNS can’t resolve on its own.

If there is specified a file path:
```
forward . /etc/resolv.conf {
	max_concurrent 1000
}
```

That means that the DNS server specified at this path on a Node (a host) will be used.

If there is an IP address:
```
forward . 8.8.8.8 1.1.1.1 {
	max_concurrent 1000
}
```

Then that means that this IP address will be used.

That DNS server needs to be able to resolve public domains like google.com. If it can’t, then that’s a problem.
## Kubernetes services DNS names
In Kubernetes, all Services are accessible via DNS at:
- \<service-name\>.\<namespace\>.svc

Any Pod can use that DNS name to connect to other Pods which uses that Service.

Kubernetes API server always uses that DNS name to communicate with resources through a Service.

If we can’t resolve that DNS name from inside of a Pod, then that indicates an issue with Kubernetes.

#Cloud #DevOps #DistributedComputing #DataEngineering 