Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Main approaches for scaling:
# 1. Scale out brokers (horizontal scaling)
Add more Kafka brokers:
```
Before:
Broker 1
Broker 2

After:
Broker 1
Broker 2
Broker 3
```

Benefits:
- more storage
- more network capacity
- more parallel processing
# 2. Increase partitions
Add more partitions to a topic:
```
Topic:

Before:
Partition 0

After:
Partition 0
Partition 1
Partition 2
```

Benefits:
- more parallelism
- more consumers can process data simultaneously
# 3. Scale consumers
Add more consumers to a consumer group:
```
Before:
Consumer A

After:
Consumer A
Consumer B
Consumer C
```

Each consumer processes different partitions.
# 4. Scale producers / applications
Increase the number of producer instances sending messages.