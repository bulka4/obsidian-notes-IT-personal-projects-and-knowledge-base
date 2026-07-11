Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a strong consistency consistency model ([[Backend Engineering - Distributed microservices - Consistency models|link]]), when one service makes a write (changes state), all the other services see this data (a new, changed state) immediately. It feels like a single shared database.
# Pros:
- Very intuitive
- Easy to reason about correctness
# Cons:
- Slow in distributed systems
- Requires coordination (latency + availability trade-off)
# Example:
- bank balance after transfer
- strict inventory systems