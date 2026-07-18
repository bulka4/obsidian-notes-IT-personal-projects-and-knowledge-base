Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
An idempotent ([[Backend Engineering - Event-driven architecture - Idempotency|link]]) producer is a Kafka producer ([[Backend Engineering - Event-driven architecture - Producer and consumer|link]]) that prevents storing duplicated messages when a producer retries sending a message (sends it multiple times).

When a response gets lost:
```
Producer
   |
send message
   |
Broker receives it
   |
Response lost
   |
Producer retries
```
when retrying to send a message without idempotency, the same message can be sent twice to a broker and broker will store duplicated message.

With an idempotent producer, Kafka detects that the retry is the same message and does not store it twice.

How it works (simplified):
- Kafka assigns the producer an ID (PID).
- Each message gets a sequence number.
- The broker uses these to detect duplicates.

Important:
- Idempotent producers prevent duplicates caused by producer retries.
- They do not make your whole application exactly-once by themselves.