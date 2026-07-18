Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Topics are techniques used in a message broker ([[Backend Engineering - Event-driven architecture - Message broker|link]]) to distribute messages ([[Backend Engineering - Event-driven architecture - Events and messages|link]]) to consumers (processes) when using an asynchronous communication ([[Backend Engineering - Asynchronous communication|link]]).

Topic is a category of messages. They are used in so called publish / subscribe communication technique (pub/sub):
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
# Consumer group
Consumer group is a group of multiple instances of the same consumer (process).