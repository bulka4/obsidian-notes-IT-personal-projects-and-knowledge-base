Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Service discovery is the mechanism that allows microservices to find and communicate with each other dynamically, without hardcoding IP addresses or hostnames.
# What service discovery does
Service discovery takes care of:
## 1. Assigning DNS names
It often automatically assigns the same DNS name to multiple instances of a services. So we can use that single DNS name to identify all the services but it doesn't tell us which one is the best to handle a request.
## 1. Instance tracking (core difference)
It knows:
- which instances exist
- which are healthy/unhealthy
- which are ready to receive traffic

DNS alone doesn’t manage health or lifecycle.
## 2. Health checking
Service discovery systems:
- continuously check if instances are alive
- remove bad instances automatically

DNS does not do health checks.
## 3. Load balancing decisions
Service discovery often participates in:
- choosing _which instance_ to call
- distributing traffic across replicas

DNS typically just returns IPs (sometimes multiple).
## 4. Dynamic registration
Services:
- register themselves at startup
- deregister on shutdown

DNS doesn’t manage this lifecycle logic by itself.
## 5. Failover awareness
If a node dies:
- service discovery updates routing immediately

DNS propagation is slow and cache-based.