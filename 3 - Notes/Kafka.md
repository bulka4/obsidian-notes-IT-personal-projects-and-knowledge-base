Tags: [[_Backend_Engineering]] [[_Kafka]]
#BackendEngineering #Kafka 

# Introduction
Apache Kafka is a distributed event streaming platform used to move, store, and process huge amounts of data in real time. It is commonly used in backend systems, data engineering, analytics, and ML pipelines.

A simple way to think about Kafka:
> Kafka is a highly scalable, fault-tolerant "log" where applications can publish events and other applications can consume them later.

More info about event-driven systems - [[Backend Engineering - Event-driven architecture (EDA)|link]].
# 1. Why Kafka exists
Traditional architecture:
```
Service A ---> Service B
Service A ---> Database
Service A ---> Analytics
Service A ---> Service C
```

Problems:
- tight coupling between services
- if one service is down, data can be lost
- hard to scale
- many direct integrations

Kafka introduces a middle layer:
```
             Kafka
               |
    -----------------------
    |          |          |
 Service A  Service B  Service C
 Producer   Consumer   Consumer
```

Now:
- producers don't know consumers
- consumers can process data independently
- data can be replayed
# Questions
- regarding the "why kafka exists" section, can you explain more problems without kafka? For example, in "if one service is down, data can be lost", you mean the producer or consumer service?