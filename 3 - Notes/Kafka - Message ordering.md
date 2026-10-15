Tags: [[__Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Message ordering means the order in which Kafka messages are stored and read ([[Software Engineering - Event-driven architecture - Ordering|link]]).

Kafka guarantees ordering only within a single partition.

To preserve ordering for related messages, send them to the same partition, usually by using the same key.