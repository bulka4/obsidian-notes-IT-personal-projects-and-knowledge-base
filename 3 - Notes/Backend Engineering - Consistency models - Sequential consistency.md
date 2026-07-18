Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a sequential consistency model ([[Backend Engineering - Distributed systems - Consistency models|link]]), when one service makes a write (changes state), all services observe writes in the same order, but not necessarily immediately. 

Different services may temporarily see older data, but they will all eventually see the same sequence of state changes. 

It does not guarantee that writes become visible in real time, only that their order is consistent for everyone.