Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Message broker integration tests verify that your application correctly interacts with a real message broker such as:
- Apache Kafka
- RabbitMQ
- Apache Pulsar

They test the interaction between:
```
Producer
    |
Message Broker
    |
Consumer
```

rather than mocking the broker (replacing the real broker with a fake object).
# What do they verify?
1. Message publishing - Send a request and verify that a message appears in the broker
2. Message consumption - Put a message into a broker and verify that a consumer processes it correctly
3. Message ordering - Check whether a consumer receive events in a correct order
4. Duplicated messages - Check whether a consumer handles duplicated events correctly
5. Retry behavior - Check whether processing succeed after broker retrying a message
6. Dead letter queues - Verify that messages that can't be processed end up in a Dead letter queue
7. Serialization - Verify that a producer format is the same as consumer expectations
8. Configuration issues:
	- wrong topic names
	- wrong queues
	- incorrect partitions
	- authentication problems
	- broker connection issues
9. Failure scenarios - Verify that the system behaves correctly in case of failures like:
	- Broker unavailable
	- Consumer crashes
	- Duplicate messages
	- Delayed messages