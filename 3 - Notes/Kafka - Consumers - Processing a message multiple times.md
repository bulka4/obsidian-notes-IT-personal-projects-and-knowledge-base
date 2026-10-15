Tags: [[__Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Kafka consumers generally provide at-least-once processing, that means that one message is processed at least once but can be processed multiple times.

That's why it is useful to make message processing by consumers idempotent ([[Software Engineering - Fault tolerance - Idempotency|link]]) so that processing the same message twice doesn't cause any issues.
# Why messages can be processed multiple times
A message can be processed multiple times because offset commit ([[Kafka - Committing offsets|link]]) and processing a message are separate operations.

For example, if we have a consumer processing a message:
```
Kafka → consumer
          ↓
     process message
          ↓
     commit Kafka offset
```

then like this can happen:
- consumer reads a message `#100` and processes it successfully
- consumer crashes before committing the offset for `#100`
- consumer restarts
- consumer resumes from the last committed offset, which is before `#100`
- consumer reads and processes message `#100` again

