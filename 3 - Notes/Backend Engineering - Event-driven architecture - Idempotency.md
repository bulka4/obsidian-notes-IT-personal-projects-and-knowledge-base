Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Idempotency in the context of application communication means that one application can send a request / message to another application multiple times and the effect will be the same as when sending it only once.

This makes retries safe in case of failure.

For example, when one application sends a request to withdraw money, each request can get assigned transaction ID. When multiple requests comes in with the same transaction ID, only one is processed and others are ignored.
# Idempotency key
Regarding APIs, idempotency key is a unique key assigned to requests. When the server tries to process the same request multiple times, it can use that key to determine whether or not the request has been already processed successfully and avoid processing it multiple times.