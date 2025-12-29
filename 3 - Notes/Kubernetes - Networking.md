Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]], [[_Kubernetes]]

# Subnets
In many Kubernetes setups (for example with Calico in BGP mode) each node in a Kubernetes cluster is a separate subnet with its own CIDR (a range of IP addresses).
# BGP
BGP is a routing protocol used by each node to tell other nodes what is its CIDR.

It is used for example by Calico.

When a Pod on one node wants to send a packet to a specific IP address which belongs to aPod on a different node, then BGP will tell it on which node that IP address can be found.

For example in case of Calico, the calico-node-xxx Pod is responsible for BGP (telling other nodes what is the CIDR of the node on which this calico-node Pod is running).
# Localhost IP address – 0.0.0.0 vs 127.0.0.1
If we bind a process to the 127.0.0.1:\<port_number\>, then we can talk to that process only from a local host, not from other servers (or pods). That's because that process will be listening only on a loopback interface.

We need to bind a process to the 0.0.0.0:\<port-number\> in order to be able to talk to it from other servers (or pods). It will be listening then on all network interfaces.