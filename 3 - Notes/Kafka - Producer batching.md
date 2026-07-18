Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
**Producer batching** is a Kafka producer optimization where the producer groups multiple messages together into a single batch before sending them to a broker.

Benefits:
- higher throughput
- fewer network requests
- better disk efficiency

Trade-off:
- Larger batches → better throughput, slightly higher latency
- Smaller batches → lower latency, lower throughput