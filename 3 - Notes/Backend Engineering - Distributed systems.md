Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Distributed microservices refers to a system where we have multiple services (applications) performing different actions and communicating with each other.

For example, we might have services like:
- Order - Where clients make orders
- Payment - Process payment for the order from the user
- Inventory - Prepare products to send to the client

In distributed microservices, there might be problems like:
- Partial failures (one service works, another doesn’t)
- Eventual consistency
- Duplicate messages
- Out-of-order events
# Related topics
1. [[Backend Engineering - Fault tolerance - Distributed systems]]
	1. [[Backend Engineering - Distributed systems - Partial failures]]
	2. [[Backend Engineering - Distributed systems - Consensus]]
2. [[Backend Engineering - Distributed systems - Service discovery]]
3. [[Backend Engineering - Distributed systems - CAP theorem]]
4. [[Backend Engineering - Distributed systems - Backpressure]]
5. [[Backend Engineering - Distributed systems - Load balancing]]
	1. [[Backend Engineering - Distributed systems - FLP impossibility]]
6. [[Backend Engineering - Distributed systems - Clock (time) synchronization]]
7. [[Backend Engineering - Distributed systems - Logical clocks (timestamps)]]
	1. [[Backend Engineering - Distributed systems - Lamport logical clock]]
	2. [[Backend Engineering - Distributed systems - Vector clocks]]
8. [[Backend Engineering - Distributed systems - Conflict resolution]]
	1. [[Backend Engineering - Conflict resolution - Last Write Wins (LWW)]]
	2. [[Backend Engineering - Conflict resolution - CRDTs (Conflict-free Replicated Data Types)]]