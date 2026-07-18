Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
A consumer group is a set of consumers that cooperate to read messages from one or more topics.

The main purpose is:
> Scale message processing horizontally while ensuring each message is processed only once per group.

Each consumer within a consumer group can process different partitions in parallel.
# Important rules
## 1. Within one consumer group, one partition is assigned to only one consumer
```
P0 -> Consumer A
P1 -> Consumer B
P2 -> Consumer C
```

This avoids duplicate processing.
## 2. Different consumer groups are independent
```
Topic: orders

payment-service group
analytics group
fraud-detection group
```

All groups receive all messages independently because each group maintains its own offsets.
## 3. Number of active consumers is limited by number of partitions
Example:
```
Topic partitions: 3
Consumers in group: 5
```

Assignment:
```
Consumer A -> P0
Consumer B -> P1
Consumer C -> P2
Consumer D -> idle
Consumer E -> idle
```

We cannot process more partitions in parallel than exist.
## 4. Rebalancing
If consumers join or leave, Kafka redistributes partitions ([[Kafka - Rebalancing|link]]).

Example:

Before:
```
A -> P0,P1
B -> P2
```

Consumer C joins:
```
A -> P0
B -> P1
C -> P2
```

This is called rebalancing.
# Related topics
- Consumer group coordinator - [[Kafka - Consumer group coordinator|link]] 