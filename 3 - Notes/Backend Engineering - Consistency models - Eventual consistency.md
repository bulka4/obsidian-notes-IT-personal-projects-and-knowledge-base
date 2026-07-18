Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In an eventual consistency model ([[Backend Engineering - Distributed systems - Consistency models|link]]), when one service makes a write (changes state), other services may temporarily see the old state. 

However, if no further writes occur, all services will eventually converge to the same, latest state.
# Pros:
- High availability
- High scalability
# Cons:
- stale reads possible
# Example:
- social feeds
- DNS propagation
- microservices data replication