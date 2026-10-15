Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Queues are techniques used in a message broker ([[Software Engineering - Event-driven architecture - Message broker|link]]) to distribute messages ([[Software Engineering - Event-driven architecture - Events and messages|link]]) to consumers (processes).

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
- Messages wait in the queue for a worker (consumer, a process) that has a capacity to process it
- Each message from the queue is processed by one worker (it can be any one) and then the message is deleted from the queue
- How a worker receives a message to process depends on the system we use, there are two options:
	- Worker pulls - The worker requests a message when it's ready to process more. The broker provides one if available.
	- Broker pushes - The broker checks whether a worker has capacity and sends messages to it, often using prefetch limits or acknowledgements to avoid overwhelming them.