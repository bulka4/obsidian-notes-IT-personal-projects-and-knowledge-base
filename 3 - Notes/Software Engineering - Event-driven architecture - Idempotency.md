Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Idempotency in the context of application communication means that processing a request / message multiple times has the same effect as processing it one.

This makes retries safe in case of failure.

For example, when one application sends a request to withdraw money, each request can get assigned transaction ID. When multiple requests comes in with the same transaction ID, only one is processed and others are ignored.
# Idempotency key
Regarding APIs, idempotency key is a unique key assigned to requests. When the server tries to process the same request multiple times, it can use that key to determine whether or not the request has been already processed successfully and avoid processing it multiple times.
# Why messages can be processed multiple times
To learn why a message can be processed multiple times, check Kafka's example - [[Kafka - Consumers - Processing a message multiple times]].