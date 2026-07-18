Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
The controller is a special broker ([[Kafka - Brokers|link]]) responsible for managing the Kafka cluster itself.

It does not handle normal message reads/writes. Instead, it manages metadata and coordination.

Responsibilities:
- broker membership (which brokers are alive)
- partition leader elections
- partition reassignments
- topic creation/deletion
- triggering updates when brokers fail
