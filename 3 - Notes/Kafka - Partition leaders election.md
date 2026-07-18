Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Partition leader election is the process Kafka uses to choose a new leader replica ([[Kafka - Leaders & followers (replication)|link]]) for a partition when the current leader fails.

The new leader is usually chosen from the ISR (In-Sync Replicas) ([[Kafka - ISR (in-sync replicas)|link]]).

There are two common cases:
1. Automatic leader election
    - Happens after broker failure.
    - Kafka automatically chooses a new leader.
2. Preferred leader election
    - Kafka tries to move leadership back to the preferred replica (usually the first replica in the assignment).
    - Used for balancing leadership across brokers.