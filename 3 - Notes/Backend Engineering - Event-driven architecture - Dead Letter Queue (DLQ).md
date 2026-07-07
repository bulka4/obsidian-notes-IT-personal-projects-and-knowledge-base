Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In asynchronous communication ([[Backend Engineering - Asynchronous communication|link]]), when processing a message ([[Backend Engineering - Event-driven architecture - Events and messages|link]]) fails multiple times in a row, it is moved aside to the Dead Letter Queue for inspection in order not to block other messages from being processed.