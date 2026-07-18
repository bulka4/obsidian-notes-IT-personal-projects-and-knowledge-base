Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
KRaft is Kafka's built-in metadata management system that replaces ZooKeeper. It handles Kafka's metadata like:
- which brokers are alive
- topic metadata
- partition assignments
- controller election information
- leader election information

Metadata is stored directly inside Kafka using the Raft consensus algorithm.

A set of controller nodes forms a controller quorum. One controller becomes the leader and manages metadata.
# Benefits
Raft provides:
- fault tolerance
- consistency
- leader election
- automatic failover
## Comparison to ZooKeeper
Benefits compared to ZooKeeper:
- Simpler deployment
- No external dependency
- Better scalability
- Easier operations
- Kafka is fully self-contained