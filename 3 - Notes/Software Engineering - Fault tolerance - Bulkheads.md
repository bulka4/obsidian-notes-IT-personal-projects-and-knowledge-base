Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Bulkheads is a technique where we assign to services limits for how much resources they can use, preventing them from using too much.

In this method, we create pools to which we assign resources and services. Services in a pool can use only the resources assigned to their pool.

Those resources can be:
- Thread pools (most common) ([[Software Engineering - Threads|link]])
- Connection pools (e.g., separate database connections)
- Network connections
- CPU or memory limits