Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
In asynchronous communication ([[Backend Engineering - Asynchronous request processing|link]]), when multiple messages ([[Software Engineering - Event-driven architecture - Events and messages|link]]) comes in, their order sometimes matter, for example:
```
Deposit 100$
Withdraw 50$
```

and processing messages in a wrong order can give wrong results.

Some brokers ([[Software Engineering - Event-driven architecture - Message broker|link]]) preserve an order of messages, some don't. Preserving an order means that messages are stored and read by consumers in the same order as they were sent to the broker by producers.

Usually, events order is preserved only within the same partition ([[Software Engineering - Event-driven architecture - Partitioning|link]]), not globally across all the partitions.