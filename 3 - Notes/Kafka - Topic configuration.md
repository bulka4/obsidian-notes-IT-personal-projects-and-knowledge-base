Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
**Topic configuration** refers to settings that control the behavior of an individual Kafka topic.

Unlike broker configuration (which affects the whole broker), topic configuration affects only a specific topic.
# Examples
- Replication factor (`replication.factor = 3`) - Controls how many copies of each partition exist.
- Retention (`retention.ms=x, retention.bytes=x`) - How long or how much data the topic keeps
- Cleanup policy (`cleanup.policy=delete`) - Controls how old data is removed (delete or log compaction ([[Kafka - Log compaction|link]]))
- Number of partitions (`partitions=x`) - Controls parallelism, throughput, consumer group scalability
- Minimum in-sync replicas (`min.insync.replicas=2`) - Kafka requires at least 2 replicas to be available for `acks=all` writes.
- Message size limits (`max.message.bytes=1000000`) - Controls the maximum size of a single message
