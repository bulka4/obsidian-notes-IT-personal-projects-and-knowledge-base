Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]

# Introduction
Service is a resource which we can assign to a Pod and it provides a static IP address to a Pod.

Pods have its own IP address, which can change over time, and Service has a separate, static IP address and it is independent on the IP address of the Pod.

In Service we can also specify a domain name for a Pod.

It also acts as a load balancer. We can have two replicas (described in the next section) of the same app (Pod), both attached to the same service, and service will redirect a request to the replica which is the least busy.
## Service types
There are different Service types:
- ClusterIP (default)
	- Exposes the Service **only inside the cluster**.
	- Clients inside the cluster can connect to myservice:port or \<ClusterIP\>:port.
- NodePort
	- Opens the Service on a static port (range: 30000–32767) on _every_ Node’s IP.
	- Clients outside the cluster can call \<NodeIP\>:\<NodePort\> and get routed to a Pod.
	- If a client wants to reach a Pod, it needs to use an IP of the Node on which this Pod is running.
- LoadBalancer
	- Provisions a cloud load balancer that routes external traffic into the Service.
	- The load balancer forwards to NodePorts under the hood, but clients see a single public IP.
- ExternalName
	- Maps the Service name to an external DNS name
- Headless
	- We setup clusterIP: None:
```
apiVersion: v1
kind: Service
spec:
	clusterIP: None
```
- When client does DNS lookup for Service name, it gets list of IP addresses of all the Pods linked to the Service.
## Labels and selector
In order to attach a Service to Pods, we need to define a label in all those Pods, for example:
```
labels:
	app: mlflow
```

And then specify in the Service a selector matching those labels:
```
selector:
	app: mlflow
```
## Cluster IP
Every Service get assigned a Cluster IP from the CIDR range (defined by the CNI when setting up a cluster).

Kube-proxy forwards requests sent to a Service’s Cluster IP, to Pods attached to that Service.

It is used only for the internal cluster communication. It can’t be reached from outside of the cluster.

That means that from inside of a Pod we can connect to other Pods using their Service’s Cluster IP, but we can’t do that from outside of a Pod. For that we need to use the External-IP
## External IP
External IP of a service is used in order to connect to the pod linked to this service.
## Finding pods linked to a service
In service we define a selector which selects pods which will be linked to this service.

If we run this command:
- kubectl get pods -n \<namespace\> --selector=\<selector\>

Then we can see which pods matches this selector. They will be linked to this service.
## Ports
In a Service we can specify which service ports correspond to which containers’ ports, for example:
```
ports:
	- protocol: TCP
	  port: 6379       # Service port
	  targetPort: 6379 # Container port
```

That means that when a client tries to reach the service on the Service port, Service will redirect the client to the container port (targetPort).

#Cloud #DevOps #DistributedComputing #DataEngineering 