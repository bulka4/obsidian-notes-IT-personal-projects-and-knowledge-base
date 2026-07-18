Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
The consumer group coordinator is the Kafka broker responsible for managing a specific consumer group.

Its responsibilities include:
- tracking group membership (which consumers are in the group)
- coordinating partition assignment
- triggering rebalances (e.g. when a new consumer joins)
- storing consumer offsets (through `__consumer_offsets`)

Important:
- There is one coordinator per consumer group.
- Different consumer groups can have different coordinators.
- The coordinator is just a normal Kafka broker; there is no separate special server.