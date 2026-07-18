Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
**Throughput and latency tuning** means adjusting Kafka settings to balance **how much data Kafka can process** (throughput) and **how quickly messages are delivered** (latency).
# Increasing throughput:
- Larger producer batches (`batch.size`)
- More batching time (`linger.ms`)
- Compression
- More partitions (more parallelism)
- More consumers in a consumer group
- More brokers
# Reducing latency:
- Smaller batches
- Lower `linger.ms`
- Less compression overhead
- Fewer processing steps
# Trade-off
Higher throughput:
- larger batches
- more waiting
- higher latency

Lower latency:
- smaller batches
- immediate sending
- lower throughput