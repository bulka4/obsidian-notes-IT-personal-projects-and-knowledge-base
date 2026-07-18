Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a causal consistency model ([[Backend Engineering - Distributed systems - Consistency models|link]]), when one service makes a write (changes state), all services observe causally related writes (writes where one causes another) in the same order, while independent writes may be seen in different orders. 

This guarantees that if one event caused another (e.g. a reply to a message), every service sees the cause before the effect, but unrelated updates do not require a global ordering.
# Example:
- “post → comment” ordering in social apps