Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
In Kafka, a **topic** is a named stream/category where messages (events) are stored.

Key points:
- Producers ([[Backend Engineering - Event-driven architecture - Producer and consumer|link]]) write messages to topics.
- Consumers read messages from topics.
- A topic is divided into partitions ([[Kafka - Partitioning|link]]) for scalability and parallel processing.
- Messages in a topic are stored for a configured retention period ([[Kafka - Retention policies|link]]) (they are not removed immediately after being consumed).
- Multiple consumer groups ([[Kafka - Consumer groups|link]]) can read the same topic independently.

Example:
```
Topic: orders

event 1: Order created
event 2: Order paid
event 3: Order shipped
```
