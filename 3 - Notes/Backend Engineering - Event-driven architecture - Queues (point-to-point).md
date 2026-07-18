Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Queues are techniques used in a message broker ([[Backend Engineering - Event-driven architecture - Message broker|link]]) to distribute messages ([[Backend Engineering - Event-driven architecture - Events and messages|link]]) to consumers (processes).

It works like this:
```
Producer
↓
Queue
↓
Worker 1
Worker 2
Worker 3
```
- Queue receives messages from a producer and stores them
- Sends each message only to one worker (consumer, a process) to process and deletes the message