Tags: [[__Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Consumers recognize an order of messages in a topic only within a single partition. If there is a message which was generated earlier but it is in another partition, it can be processed later.

For example, we might have messages generated in this order:
```
message 1
message 2
message 3
```

but they go to different partitions:
```
Partition 0:
message 1
message 3

Partition 1:
message 2
```

And a consumer can process messages from the Partition 0 first and then the message from the Partition 1, even though the message 2 from the Partition 1 was generated before the message 3 from the Partition 0.