Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
In Kafka, rebalancing is the process of redistributing work or leadership assignments when the cluster state changes (e.g. a new consumer is added)
# Common types
## 1. Consumer group rebalancing
Redistributes partitions among consumers in a consumer group when a new consumer appears, for example:
Before:
```
Topic partitions:

P0 → Consumer A
P1 → Consumer A
P2 → Consumer B
```

Consumer C joins:
```
P0 → Consumer A
P1 → Consumer B
P2 → Consumer C
```

Kafka reassigns partitions so work is balanced.

Triggered by:
- consumer joins/leaves
- consumer failure
- topic partition changes
## 2. Partition leadership rebalancing
Redistributes which brokers are leaders for partitions.

Example:

Before:
```
Broker 1:
  P0 leader
  P1 leader
  P2 leader
```

After:
```
Broker 1:
  P0 leader

Broker 2:
  P1 leader

Broker 3:
  P2 leader
```

This prevents one broker from handling all traffic.

It is triggered by:
- Adding a new broker
- broker failures (leader election)
- manual partition reassignment
- preferred leader election