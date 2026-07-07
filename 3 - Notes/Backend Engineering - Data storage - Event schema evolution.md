Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Event schema evolution / versioning is used in event sourcing ([[Backend Engineering - Data storage - Event sourcing|link]]). It is how we handle changes in the structure of events over time in an event-driven or event-sourced system without breaking old data or consumers.

Events are usually:
- stored for a long time (event sourcing), or
- consumed by many services (EDA)

But software changes:
- fields get added/removed
- meanings change
- formats evolve

So we need a way to ensure:
> old events still work with new code, and new events don’t break old consumers.