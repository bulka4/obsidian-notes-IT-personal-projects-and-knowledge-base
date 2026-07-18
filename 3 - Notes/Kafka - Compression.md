Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Compression reduces the size of messages sent from producers to Kafka brokers and stored on disk.

Compression is usually applied to producer batches ([[Kafka - Producer batching|link]]), so it works well together with batching.

Benefits:
- less network traffic
- less disk storage
- higher throughput

Common compression types:
- `gzip` → better compression, slower
- `snappy` → fast, moderate compression
- `lz4` → fast, good balance
- `zstd` → high compression and good performance