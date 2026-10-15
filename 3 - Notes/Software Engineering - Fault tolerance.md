Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Fault tolerance is the ability of a system to continue working despite failures.
# Handling errors
To handle errors we can use:
- **Timeouts** ([[Software Engineering - Fault tolerance - Timeouts|link]]) - Setting up a limit for how long a system waits for a response from another system. After that time, sending the request fails.
- **Retries with backoff** ([[Software Engineering - Fault tolerance - Retries with backoff|link]]) - When a request fails, send another one after some time. After every request, we wait longer then previously.
- **Circuit breakers** ([[Software Engineering - Fault tolerance - Circuit breakers|link]]) - When requests continue failing for a long time, then for some time, every time we want to make a request, we perform some other, alternative action instead
- **Idempotency** ([[Software Engineering - Fault tolerance - Idempotency|link]]) - Performing the same operation multiple times has the same final effect as performing it once. This makes retries having a correct result.
- **Bulkheads** ([[Software Engineering - Fault tolerance - Bulkheads|link]]) - Assign to services limits for how much resources they can use, preventing them from using too much
# Checking health of services
- **Health checks** - verifying whether a service instance is healthy and able to handle requests (one service asks another one about its health). Popular checks include:
	- Liveness check - check whether a service runs
	- Readiness check - check whether a service is ready to handle requests from clients
- **Heartbeats** - A service sends periodically signals informing that it runs and works correctly
# Redundancy and failover
- **Redundancy** ([[Software Engineering - Fault tolerance - Redundancy|link]]) - having extra components or resources so that in case of a failure they can start be using instead of failed ones and the system can continue working
	- **Replication** ([[Software Engineering - Fault tolerance - Replication|link]]) - one method for redundancy - create copies of a service which can take over in case of failure
- **Failover** ([[Software Engineering - Fault tolerance - Failover|link]]) - switch from a failed component to a healthy backup component to keep the system running
# Distributed systems
## Partial failures
Partial failures happen when some parts of a distributed system ([[Backend Engineering - Distributed systems|link]]) fail while others keep working.

This can lead for example to inconsistent state (data) ([[Databases - Data consistency|link]]) - e.g. a payment succeeded but an order not updated

More information can be found here - [[Backend Engineering - Distributed systems - Partial failures]].
## Consensus
Consensus is a mechanism that allows multiple nodes (servers) in a distributed system to agree on for example:
- what operations were performed (data changes)
- in what order 
- what is the latest state (how data should look like)

even when some nodes or a network fail, nodes can't communicate or some messages in an event-driven system ([[Software Engineering - Event-driven architecture (EDA)|link]]) are delayed.

More information can be found here - [[Backend Engineering - Distributed systems - Consensus]].
# Event-driven systems
More information about handling failures in event-driven systems - [[Software Engineering - Fault tolerance - Event-driven architecture]].
# Related topics
1. [[Software Engineering - Fault tolerance - Timeouts]]
2. [[Software Engineering - Fault tolerance - Retries with backoff]]
3. [[Software Engineering - Fault tolerance - Circuit breakers]]
4. [[Software Engineering - Fault tolerance - Idempotency]]
5. [[Software Engineering - Fault tolerance - Bulkheads]]
6. [[Software Engineering - Fault tolerance - Health checks]]
	1. [[Software Engineering - Deployment - Readiness & liveness probes]]
7. [[Software Engineering - Fault tolerance - Heartbeats]]
8. [[Software Engineering - Fault tolerance - Redundancy]]
	1. [[Software Engineering - Fault tolerance - Replication]]
9. [[Software Engineering - Fault tolerance - Failover]]
10. [[Backend Engineering - Fault tolerance - Distributed systems]]
	1. [[Backend Engineering - Distributed systems - Partial failures]]
	2. [[Backend Engineering - Distributed systems - Consensus]]
11. [[Software Engineering - Fault tolerance - Event-driven architecture]]
	1. [[Software Engineering - Event-driven architecture - Dead Letter Queue (DLQ)]]
	2. [[Software Engineering - Event-driven architecture - Idempotency]]
	3. [[Software Engineering - Event-driven architecture - Ordering]]
	4. [[Software Engineering - Event-driven architecture - Delivery Guarantees]]