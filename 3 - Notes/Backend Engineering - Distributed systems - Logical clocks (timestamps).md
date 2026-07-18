Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Logical clocks are a method used to order events in distributed systems ([[Backend Engineering - Distributed systems|link]]) without relying on physical time. 

We use them because time on different servers might not be synchronized perfectly, so for example we could have a situation where:
- When on server A is 10:00:05, on server B it is 10:00:02
- Server A sends a message at 10:00:05 according to its time
- Server B receives that message at 10:00:03 according to its time

Example techniques of logical clocks include:
- Lamport clocks ([[Backend Engineering - Distributed systems - Lamport logical clock|link]])
- Vector clocks ([[Backend Engineering - Distributed systems - Vector clocks|link]])