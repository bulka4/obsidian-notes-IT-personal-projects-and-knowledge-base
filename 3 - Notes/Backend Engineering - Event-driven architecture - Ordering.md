Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In asynchronous communication ([[Backend Engineering - Asynchronous communication|link]]), when multiple messages ([[Backend Engineering - Event-driven architecture - Events and messages|link]]) comes in, their order sometimes matter, for example:
```
Deposit 100$
Withdraw 50$
```

Some brokers ([[Backend Engineering - Event-driven architecture - Message broker|link]]) preserve an order of messages, some don't.

Usually, events order is preserved only within the same partition ([[Backend Engineering - Event-driven architecture - Partitioning|link]]), not globally across all the partitions.