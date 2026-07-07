Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Eventual consistency is a consistency model ([[Backend Engineering - Distributed microservices - Consistency models|link]]) where if nothing new happens, all nodes will eventually converge:
- Temporary inconsistencies are allowed
- System becomes consistent over time
# Pros:
- High availability
- High scalability
# Cons:
- stale reads possible
# Example:
- social feeds
- DNS propagation
- microservices data replication