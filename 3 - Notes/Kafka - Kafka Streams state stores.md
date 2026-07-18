Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka Streams state stores are local storage areas used by Kafka Streams applications ([[Kafka - Kafka Streams|link]]) (applications that read from topics and write to it) to keep state (intermediate results) while processing data.

Kafka Streams is not always stateless. Many operations need memory of previous messages.
# Example
Counting events - To calculate counts, the application needs to remember previous counts. A state store can keep this data
# Who provides a state store
Kafka Streams itself provides and manages the state store:
- The state store is usually stored locally on the machine/container running the Kafka Streams application (often using RocksDB).
- Kafka Streams automatically creates a changelog topic in Kafka to back it up and restore it.
# Types of state stores
- Key-value stores → store data by key
- Window stores → store data for time windows
- Session stores → store user sessions
# Reliability
State stores are backed up using Kafka topics called changelog topics.

If the Streams application crashes, a new instance can read from the changelog topic and rebuild a state store.