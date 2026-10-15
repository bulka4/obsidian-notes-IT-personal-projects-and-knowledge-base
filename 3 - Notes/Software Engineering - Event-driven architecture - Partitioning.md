Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Events are not processed as one global stream. Instead, they are split into partitions which are groups of messages. 

Each topic ([[Software Engineering - Event-driven architecture - pub-sub (topics and consumer groups)|link]]) is split into partitions and different partitions can be stored in message brokers on different servers.
# Why partition?
- scale horizontally (many consumers)
- parallel processing
- avoid a single bottleneck
# How partitioning works (e.g., Kafka-style systems)
We choose a partition key, such as:
- `orderId`
- `userId`
- `accountId`

All events with the same key go to the same partition.
# Related topics
- Replication - [[Software Engineering - Event-driven architecture - Partition replication|link]] 