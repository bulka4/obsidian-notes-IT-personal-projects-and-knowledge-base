Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Conflict resolution is the mechanism a distributed system uses to decide what to do when multiple replicas have different versions of the same data.

This problem appears because of:
- replication
- network partitions
- offline clients
- concurrent writes

For example, when we have two database replicas (using a leaderless replication) and both replicas accept different writes so they end up with different data, for example:
```
Replica A: name = Alice
Replica B: name = Bob
```

later on we need to synchronize all the replicas and figure out which value is correct.
# Methods
Common methods include:
- Last Write Wins (LWW) - [[Backend Engineering - Conflict resolution - Last Write Wins (LWW)|link]] 
- CRDTs (Conflict-free Replicated Data Types) - [[Backend Engineering - Conflict resolution - CRDTs (Conflict-free Replicated Data Types)|link]] 
# Questions
- Can you explain more Multi-leader / leaderless replication?