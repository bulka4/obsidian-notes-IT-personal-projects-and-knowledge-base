Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
An offset is a number assigned to each message within a partition ([[Kafka - Partitioning|link]]):
```
Messages:   A   B   C   D   E
Offsets:    0   1   2   3   4
                    ↑
             last committed
```

Every time a consumer from a consumer group ([[Kafka - Consumer groups|link]]) processes a message, it commits the offset of that message, i.e. Kafka saves information that the message with this offset was the last processed message for this consumer group.

When a consumer crashes, it can then recall at which offset it has finished and continue processing messages from that offset.

For example, store:
> I have processed messages up to offset 2

If it crashes, restart from:
> Offset 3
# Related topics
- Consumer offsets - [[Kafka - Consumer offsets|link]] 