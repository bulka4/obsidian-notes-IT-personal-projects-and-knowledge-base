Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Dead letter queues (DLQs) ([[Backend Engineering - Event-driven architecture - Dead Letter Queue (DLQ)|link]]) are places where messages that cannot be successfully processed are sent so they do not block normal processing.

Kafka does not have a built-in DLQ feature like some traditional message queues, but it is a common pattern implemented using another Kafka topic.

When a consumer tries to process a message from a topic and it fails, consumer moves it to a DLQ topic with additional information about the error.