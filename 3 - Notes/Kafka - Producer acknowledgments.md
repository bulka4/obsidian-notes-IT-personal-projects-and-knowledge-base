Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Producer acknowledgments (`acks`) define how much confirmation a Kafka producer requires from the Kafka cluster before considering a message successfully written.

They control the trade-off between speed and durability.
# Options
## No confirmation
This is the `acks=0` option. Producer sends the message and does not wait:
- Fastest
- Lowest reliability
- Message can be lost if the broker fails
## Leader confirms
This is the `acks=1` option. Producer waits until the leader replica writes the message:
- Good performance
- If the leader crashes before followers replicate, the message may be lost
## all in-sync replicas confirm
This is the `acks=all` (or `acks=-1`) option. Producer waits until all replicas in the ISR (In-Sync Replicas) have stored the message:
- Highest durability
- Slower
- Usually used for important data