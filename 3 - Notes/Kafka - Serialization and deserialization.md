Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Serialization and deserialization are the processes of converting data between application objects and Kafka messages.

**Kafka stores messages always as bytes (in a binary format).**

The process is like this:
- Serialization
	- Producer converts an object into bytes before sending to Kafka
	- Data is saved in a binary format in Kafka's topic
- Deserialization
	- Consumer reads data from Kafka's topic in a binary format and converts it back into an object (deserializes it)
