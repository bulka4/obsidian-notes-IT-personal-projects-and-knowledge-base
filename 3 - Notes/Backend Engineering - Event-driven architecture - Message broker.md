Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
A message broker is used for asynchronous communication ([[Backend Engineering - Asynchronous communication|link]]). It receives messages ([[Backend Engineering - Event-driven architecture - Events and messages|link]]) from a client (producer), stores them and forwards to other, multiple services (consumers). Popular tools include:
- Apache Kafka
- RabbitMQ
- Apache Pulsar
- Amazon SQS
## Messages and events
A message is simply data, usually:
- JSON
- Protocol Buffers
- Avro

Messages describes events.