Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
In Kafka, topics ([[Kafka - Topics|link]]) are split into partitions where each partition contains a subset of all events:
- Each message is replicated and stored in a different partition
- Each partition can be stored on a different server and processed independently (in parallel)
- Each event is stored in a few partitions stored on different servers in case we loose a server
# Ordering
Kafka guarantees event ordering only within a single partition, not across the whole topic.
# How messages are assigned to partitions
Kafka hashes chosen key (uses a hash function on a chosen column) and messages with the same hash (output of a hash function) goes to the same partition.