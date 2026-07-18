Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Consistency models define how and when state ([[Backend Engineering - Distributed systems - State|link]]) changes become visible across the system (services) after a write.
# Why it matters
We care about consistency models because in a distributed system different parts of the system may not see data changes at the same time. 

The consistency model defines what guarantees the system provides about data visibility across the system.

The choice affects:
## 1. Correctness
Some systems require everyone to see the latest data immediately.

Examples:
- bank balance
- inventory count (to avoid overselling)

→ need stronger consistency.
## 2. Performance and scalability
Strong consistency requires coordination between nodes, which causes:
- higher latency
- more communication
- lower availability during failures

Weaker consistency allows:
- faster writes
- better scalability
- higher availability
## 3. User experience
Sometimes temporary inconsistency is acceptable.

Examples:
- social media likes
- view counters
- recommendations

A user seeing "100 likes" while another node has "101 likes" briefly is usually fine.
## 4. System design decisions
The consistency model tells developers what they can assume.

For example:

**Strong consistency:**
> "After I update my profile name, everyone immediately sees the new name."

**Eventual consistency:**
> "After I update my profile name, some users may temporarily see the old name, but eventually everyone sees the new one."
# How data can be inconsistent
In distributed systems, there usually isn't one single storage location that all services read from.

So there can be a situation that one service uses the latest data, while others still uses the old one.

For example, if we have a database with 3 replicas:
```
Service A
   |
   v
Database node 1   (leader)
   |
   +----> Database node 2 (replica)
   |
   +----> Database node 3 (replica)
```

Initial state:
```
Node 1: balance = 100
Node 2: balance = 100
Node 3: balance = 100
```

Service A writes:
```
balance = 120
```

The write reaches Node 1:
```
Node 1: balance = 120
Node 2: balance = 100
Node 3: balance = 100
```

Until replication finishes, services reading from Node 2 or Node 3 still see the old value.
# Example
- User data gets updated in a database - That's a state change (data is a state).
- An event `OrderCreated` gets emitted - That's a state change and the current state is a result of applying all the events emitted so far, i.e. all the data about clients and their orders.
# Consistency model types
- Strong consistency - [[Backend Engineering - Consistency models - Strong consistency|link]] 
- Sequential consistency - [[Backend Engineering - Consistency models - Sequential consistency|link]] 
- Causal consistency - [[Backend Engineering - Consistency models - Causal consistency|link]] 
- Eventual consistency - [[Backend Engineering - Consistency models - Eventual consistency|link]] 
- Weak consistency - [[Backend Engineering - Consistency models - Weak consistency|link]] 
- Read-your-writes consistency - [[Backend Engineering - Consistency models - Read-your-writes  consistency|link]] 
- Monotonic reads consistency - [[Backend Engineering - Consistency models - Monotonic reads consistency|link]] 
- Session consistency - [[Backend Engineering - Consistency models - Session consistency|link]] 