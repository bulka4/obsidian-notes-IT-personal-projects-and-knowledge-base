Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
In the publish / subscribe communication technique (pub/sub), we have:
- Topics - a category (collection) of messages. It is used  in a message broker ([[Software Engineering - Event-driven architecture - Message broker|link]]) to distribute messages ([[Software Engineering - Event-driven architecture - Events and messages|link]]) to consumers (processes) when using an asynchronous communication ([[Backend Engineering - Asynchronous request processing|link]]).
- Consumer groups - group of multiple instances of the same consumer (process) that processes messages from a specific topic.

In this technique:
```
Producer
↓
Topic
↓
Consumer group 1
Consumer group 2
Consumer group 3
```
- Producer sends messages to a topic where they are stored
- Each message from a topic is read by each consumer group independently
	- Consumer group is a group of multiple instances of the same consumer (process)
- Within a consumer group, only one instance processes a message
- Messages in a topic are removed after some time