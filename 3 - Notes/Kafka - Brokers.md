Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
A broker is a Kafka server (a type of a message broker ([[Backend Engineering - Event-driven architecture - Message broker|link]])). A Kafka cluster consists of multiple brokers.

Brokers are responsible for:
- storing partitions and messages
- receiving messages from producers
- serving messages to consumers
- replicating data to other brokers
- coordinating partition leaders

Producers and consumers usually communicate with the broker ([[Kafka - Leaders & followers (replication)|link]]) that hosts the leader replica of a partition.
# Related topics
- Controller ([[Kafka - Controller|link]])