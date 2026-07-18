Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Broker configuration refers to the settings that control how a Kafka broker behaves.

A Kafka broker has a configuration file (usually `server.properties`) containing settings for networking, storage, replication, performance, and security.
# Examples
- Identity & cluster connection (`broker.id=1`) - Unique identifier of the broker.
- Network (`listeners=PLAINTEXT://:9092`) - Defines where the broker accepts connections. Controls:
	- producer connections
	- consumer connections
	- inter-broker communication
- Storage (`log.dirs=/var/lib/kafka/data`) - Where Kafka stores partition logs.
- Replication
	- `default.replication.factor=3` - Default number of replicas for newly created topics.
	- `min.insync.replicas=2` - Minimum number of replicas that must be in sync for writes with `acks=all`.
- Retention (`log.retention.hours=168`) - How long messages are kept.
- Performance (`num.network.threads=3, num.io.threads=8`) - Control threads handling network requests and disk operations.
- Security (`ssl.*, sasl.*`) - Encryption, authentication