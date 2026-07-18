Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka Connect is a Kafka component used to move data between Kafka and external systems without writing custom integration code. It is an application that we download and run.

It can be used:
- by external systems to save messages in a Kafka topic (we can save messages from a database or from a script)
- or to read messages from a Kafka topic (we can read them directly into a database or into a script)
# How it is used
- Kafka Connect is an application that we download and run
- We install different connector plugins which are used to connect to different systems
- Kafka Connect loads a connector plugin (code to be used)
- We send a configuration file through Kafka Connect's REST API to create a connector instance 
- A connector instance runs inside Kafka Connect and continuously moves data

So we don't write code like with producer/consumer APIs ([[Kafka - Producer & Consumer APIs|link]]).
# Connectors
There are two types of connectors:
- Source connectors - Used to move data into a Kafka topic
- Sink connectors - Used to read data from a Kafka topic