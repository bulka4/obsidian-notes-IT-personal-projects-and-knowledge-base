Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Outbox pattern is a data consistency pattern ([[Backend Engineering - Distributed systems - Data Consistency Patterns (distributed transactions)|link]]) used in event-driven systems ([[Backend Engineering - Event-driven architecture (EDA)|link]]) when we need to:
- update database
- send an event ([[Backend Engineering - Event-driven architecture - Events and messages|link]])

It can help with a problem when:
- DB update succeeds
- event publishing fails
It can prevent system inconsistency in that scenario.

In this pattern, we:
- update database
- save in an Outbox table a message describing the event
as the same transaction (so either both fails or both succeeds).

Then we can send the message to other services later, whenever that is possible (we can make multiple attempts if it fails).

Thanks to this, once the transaction commits, we can't loose information about the event.
# How it works
## Step 1: transaction
```
Order table updated
Outbox table updated (event stored)
```
## Step 2: async publisher
A background process:
```
reads Outbox table
publishes event to Kafka / broker
```
# Why it matters
- no lost events
- atomicity between DB + events
- very common in event-driven systems

Used with:
- Apache Kafka