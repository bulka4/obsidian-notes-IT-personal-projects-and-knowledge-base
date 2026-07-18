Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Last Write Wins (LWW) is a method of conflict resolution ([[Backend Engineering - Distributed systems - Conflict resolution|link]]). It keeps the value with the newest timestamp.
# Problems
## Data lost
Using LWW we might loose some data in situations when during merging data from two replicas we need to include data from both replicas, not choosing only one.

For example, if we have a data about a shopping cart:
```
Replica A:
Cart: + laptop

Replica B:
Cart: + phone
```

After merging using LWW, we will end up with:
```
Cart: + laptop
```

while we need data from both replicas:
```
Cart: 
	+ laptop
	+ phone
```
## Clock accuracy
LWW depends on timestamps and times on different servers can be desynchronized ([[Backend Engineering - Distributed systems - Clock synchronization|link]]).