Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
An offset is a number assigned to each message within a partition ([[Kafka - Partitioning|link]]).

A consumer ([[Backend Engineering - Event-driven architecture - Producer and consumer|link]]) can store an information about up to which offset it processed messages and when it crashes, it can then recall at which offset it has finished and continue processing messages from that offset.

For example, store:
> I have processed messages up to offset 2

If it crashes, restart from:
> Offset 3
# Related topics
- Consumer offsets - [[Kafka - Consumer offsets|link]] 
- Committing consumed offset - [[Kafka - Committing consumed offset|link]] 