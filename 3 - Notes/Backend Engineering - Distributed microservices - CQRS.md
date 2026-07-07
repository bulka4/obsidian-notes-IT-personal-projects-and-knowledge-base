Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
CQRS is a technique often used in distributed microservices ([[Backend Engineering - Distributed microservices|link]]) and event-driven systems ([[Backend Engineering - Asynchronous communication|link]]). 

It is useful when reads and writes have different needs:
- writes need consistency
- reads need speed and scalability

This technique separates writes and reads responsibilities. This separation might be implemented using different:
- Data models (tables used for writes and reads)
- Storage systems
- APIs / code used for writing and reading
for writes and reads.

It optimizes writes for correctness and reads for performance.
# Structure
By write / read sides we mean parts of the system responsible for writing / reading data, e.g. data models, APIs and all the code.
## Write side (Commands)
**Responsibilities**:
- validate input
- enforce business rules
- update database
- emit events (often)

**Example**:
```
POST /orders 
→ create order 
→ update Orders table 
→ publish OrderCreated event
```

This side is focused on:
> “Make the change happen correctly”
## Read side (Queries)
**Responsibilities**:
- serve fast reads
- optimized for queries
- often denormalized data

**Example**:
```
GET /orders/123 
→ read from read model (optimized table)
```

This side is focused on:
> “Return data fast and efficiently”
# Typical architecture
```
Command → Write DB → Event → Read DB updated → Query uses Read DB
```

Often combined with event-driven systems ([[Backend Engineering - Asynchronous communication|link]]).