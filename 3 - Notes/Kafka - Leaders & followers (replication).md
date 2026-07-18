Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
In Kafka, leaders and followers are different replicas of the same event ([[Kafka - Partitioning|link]]) - there is one leader with the latest data and multiple followers that copies data from the leader.
# Leader
The leader handles all reads and writes for the partition. Consumers also usually read from the leader.
# Followers
Followers continuously copy data from the leader. They exist for fault tolerance (in case one server crashes and we loose a partition).
# Failure
When a broker that stores a leader partition crashes, Kafka elects one of the up-to-date followers to become the new leader.

This allows the system to continue operating without data loss (assuming proper replication settings).
# Related topics
- Replication factor - [[Kafka - Replication factor|link]] 