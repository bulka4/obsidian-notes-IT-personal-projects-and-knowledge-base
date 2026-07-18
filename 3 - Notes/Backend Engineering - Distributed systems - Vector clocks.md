Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Vector clock is an example of a logical clock ([[Backend Engineering - Distributed systems - Logical clocks (timestamps)|link]]). It is similar to Lamport clocks ([[Backend Engineering - Distributed systems - Lamport logical clock|link]]), it is also a logical clock counter but each node stores a vector of timestamps from every node:
```
[A=5, B=2, C=9]
```

So we know what was a timestamp on every node when an event happened. Thanks to this, we can compare events between nodes which happened earlier, for example that an event A on one server happened before an event B on another server.