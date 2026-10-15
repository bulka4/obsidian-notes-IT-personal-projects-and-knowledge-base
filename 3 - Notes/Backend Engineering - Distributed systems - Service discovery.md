Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Service discovery is a mechanism by which a service or client finds the network address of another service it wants to communicate with.
# Common service discovery approaches
## DNS-based 
Service discovery mechanism automatically assigns the same DNS name to multiple instances of a services. So we can use that single DNS name to identify all the instances of a service but it doesn't tell us which one is the best to handle a request.
## Registry-based
Instances register with a registry, and clients or proxies query it. Examples include Consul and service registries used with Eureka.