Tags: [[_Backend_Engineering]]
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
1. State - [[Backend Engineering - Distributed systems - State|link]] 
2. Partial failures - [[Backend Engineering - Distributed systems - Partial failures|link]] 
3. Service discovery - [[Backend Engineering - Distributed systems - Service discovery|link]] 
4. CAP theorem - [[Backend Engineering - Distributed systems - CAP theorem|link]] 
5. Backpressure - [[Backend Engineering - Distributed systems - Backpressure|link]] 
6. Load balancing - [[Backend Engineering - Distributed systems - Load balancing|link]] 
7. Consensus - [[Backend Engineering - Distributed systems - Consensus|link]] 
	1. FLP impossibility - [[Backend Engineering - Distributed systems - FLP impossibility|link]] 
8. Clock synchronization - [[Backend Engineering - Distributed systems - Clock synchronization|link]] 
9. Logical clocks (timestamps) - [[Backend Engineering - Distributed systems - Logical clocks (timestamps)|link]] 
	1. Lamport logical clock - [[Backend Engineering - Distributed systems - Lamport logical clock|link]] 
	2. Vector clocks - [[Backend Engineering - Distributed systems - Vector clocks|link]] 
10. Conflict resolution - [[Backend Engineering - Distributed systems - Conflict resolution|link]] 
	1. Last Write Wins (LWW) - [[Backend Engineering - Conflict resolution - Last Write Wins (LWW)|link]] 
	2. CRDTs (Conflict-free Replicated Data Types) - [[Backend Engineering - Conflict resolution - CRDTs (Conflict-free Replicated Data Types)|link]] 