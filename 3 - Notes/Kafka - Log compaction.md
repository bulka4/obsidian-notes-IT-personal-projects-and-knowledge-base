Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Log compaction is a Kafka retention strategy where Kafka keeps only the latest message for each key instead of deleting messages purely based on age.

Once in a while Kafka removes all the messages except for the latest one for each key value in each partition.

It is different than a standard retention where each message is deleted after a specific time.

It is useful when a topic represents a current state, not a history of events, for example:
- user profiles
- account balances
- configuration
- feature stores for ML

Important:
- Compaction does not happen immediately. Kafka cleans old records in the background.
- Messages without keys are not useful for compaction.
- Kafka keeps ordering within partitions.
- Compaction is different from normal retention.