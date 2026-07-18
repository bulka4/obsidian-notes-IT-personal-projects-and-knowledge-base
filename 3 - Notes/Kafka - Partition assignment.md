Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Partition assignment is the process of Kafka deciding which consumer in a consumer group reads which partitions.

Kafka's group coordinator performs this assignment.

It happens when:
- consumers join or leave a group
- partitions change
- a rebalance is triggered

The goal is to:
- distribute work across consumers
- ensure each partition has only one consumer within the group

Important:
- Assignment is per consumer group.
- Different consumer groups can have completely different assignments for the same topic.