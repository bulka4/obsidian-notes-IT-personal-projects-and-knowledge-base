Tags: [[__Machine_Learning_Engineering]], [[_Ray]]
#MLEngineering #Ray 

# Introduction
Ray uses a shared, in-memory object store (Plasma) to pass data between processes and nodes.

Data goes through the object store whenever we:
- Pass data to a remote task/actor
- Return results from `.remote()`
- Use Ray Data blocks

Data is serialized ([[Ray - Serialization|link]]) before being written into the object store.