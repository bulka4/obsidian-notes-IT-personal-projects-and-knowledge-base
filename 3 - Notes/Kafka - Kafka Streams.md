Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka Streams is a Kafka library (Java/Scala) for processing data from Kafka topics and writing results back to Kafka topics.

It allows us to build real-time stream processing applications without needing a separate processing engine like Spark Streaming or Flink.

Common operations:
- Filtering
- aggregation
- joins (combine two streams (events from two topics))
- mapping / transformation

It is similar to producer/consumer APIs ([[Kafka - Producer & Consumer APIs|link]]) but Kafka Streams is higher-level with more abstractions. Using producer/consumer APIs, we have more flexibility when it comes to what do we do with the data.