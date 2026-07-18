Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Bulkheads is a technique of preventing services from using too much resources.

In this method, we create pools to which we assign resources and services. Services in a pool can use only the resources assigned to their pool.

Those resources can be:
- Thread pools (most common) ([[Software Engineering - Threads|link]])
- Connection pools (e.g., separate database connections)
- Network connections
- CPU or memory limits