Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Event-driven architecture is one of ways to implement asynchronous processing.

In this architecture services send messages about events to each other:
- requester (a service) publishes an event
- Message broker receives and stores a message with information about the event
- Multiple other services receives and processes the message
- The result of processing the message is not sent back to the requester immediately, only a confirmation about receiving the message.

More information about it can be found here - [[Software Engineering - Event-driven architecture (EDA)]].