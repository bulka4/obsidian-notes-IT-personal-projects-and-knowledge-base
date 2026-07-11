Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a weak consistency model ([[Backend Engineering - Distributed microservices - Consistency models|link]]), when one service makes a write (changes state), there are no guarantees about when or even if other services will observe the updated state at all.

Different services may see different versions of the data for an arbitrary amount of time.

It is often used in caching systems.