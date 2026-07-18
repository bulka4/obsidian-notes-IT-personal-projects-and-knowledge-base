Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
ZooKeeper is used to handle Kafka's metadata:
- which brokers are alive
- topic metadata
- partition assignments
- controller election information
- leader election information

Problems:
- Extra system to deploy and maintain
- More operational complexity
- Metadata operations could become a bottleneck