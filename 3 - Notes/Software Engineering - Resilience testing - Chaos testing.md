Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Chaos testing is a resilience testing practice where you deliberately introduce failures into a system to discover weaknesses and verify that it can recover.

The idea:
> "Assume failures will happen; create them intentionally before they happen in production."
# Examples of chaos experiments
## Kill a service instance
```
Before:

Load Balancer
      |
  Service A (3 replicas)


Chaos experiment:

Kill 1 replica ❌


Expected:

Service A continues working with 2 replicas
```
## Simulate infrastructure failures
Examples:
- terminate a server/VM
- restart Kubernetes pods
- make a database unavailable
- introduce network latency
- block communication between services

Check:
- automatic recovery
- failover
- data consistency
- user impact
## Example in Kubernetes
Experiment:
```
Delete 20% of application pods
```

Expected behavior:
```
Traffic redirected automatically
New pods created
No downtime
```