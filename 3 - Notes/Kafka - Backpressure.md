Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Backpressure ([[Backend Engineering - Distributed systems - Backpressure|link]]) is implemented in Kafka by accumulating messages in a topic.

This creates consumer lag:
```
Produced offset: 1,000,000 (how many messages a producer has sent)
Consumed offset:   900,000 (how many messages a consumer has processed)

Lag = 100,000
```
# Ways to handle backpressure in Kafka
## Increase consumers (within the number of partitions)
```
More consumers
      ↓
More parallel processing
```
## Increase partitions (allows more consumers)
```
3 partitions → 3 consumers
10 partitions → up to 10 consumers
```
## Tune consumers
- increase batch sizes
- optimize processing time
- adjust polling settings
## Slow down producers (application-level throttling)
```
Producer rate ↓
```
## Scale downstream systems:
Example:
```
Kafka
  |
Consumer
  |
Database  ← bottleneck

Increase database capacity
```