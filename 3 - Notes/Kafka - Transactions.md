Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka transactions allow a producer to write multiple messages atomically — either all writes succeed, or none become visible to consumers.
# Example
A common Kafka Streams example:
```
Input topic
    |
    v
Process event
    |
    +--> Write output topic
    |
    +--> Commit consumed offset
```

Kafka can make these two actions atomic:
1. Writing the processed result to a topic ([[Kafka - Topics|link]])
2. Committing the consumer offset ([[Kafka - Committing consumed offset|link]])

So after a failure, Kafka does not:
- write the output but fail to commit the offset (causing duplicates)
- commit the offset but fail to write the output (causing data loss)
# Common usage
Transactions are used together with:
- Idempotent producers ([[Kafka - Idempotent producers|link]]) (required internally)
- `acks=all` ([[Kafka - Producer acknowledgments|link]])
- `isolation.level=read_committed` (consumer reads only committed transactional messages)