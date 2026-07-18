Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Partition reassignment is the process of moving partitions (or their replicas) between brokers.

It is used when we need to change where Kafka stores partition data.
# Common reasons
- adding a new broker → distribute data/load
- removing a broker → move its partitions away
- fixing uneven partition distribution
- changing replication factor
# During reassignment Kafka
1. copies partition data to new brokers
2. updates replica assignments
3. may elect new leaders