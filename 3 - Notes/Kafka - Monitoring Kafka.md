Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Areas to monitor
## 1. Broker health
Checks whether brokers are working correctly.

Examples:
- broker availability
- CPU usage
- memory usage
- disk usage
- network traffic
## 2. Topic and partition metrics
Monitor data distribution and storage.

Examples:
- number of partitions
- partition size
- replication status
- under-replicated partitions

Important metric:
```
Under-replicated partitions > 0

→ some replicas are not synchronized
→ possible reliability issue
```
## 3. Consumer lag
One of the most important metrics.

It measures how far behind consumers are:
```
Latest message offset: 10000
Consumer offset:         8000

Lag = 2000 messages
```

High lag means consumers cannot keep up.
## 4. Producer metrics
Monitor:
- message throughput
- request latency
- failed sends
- retries
- error rates
## 5. Replication metrics
Monitor:
- ISR size
- leader changes
- replica synchronization
# Metrics
[[Kafka - Metrics]].