Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Event schema evolution / versioning is used in event sourcing ([[Software Engineering - Architecture patterns - Event sourcing|link]]) and event-driven architecture (EDA - [[Backend Engineering - Event-driven architecture (EDA)|link]]). 

It is a way how we handle changes in the structure of events over time without breaking old data or consumers.

Events are usually:
- stored for a long time (event sourcing), or
- consumed by many services (EDA)

But software changes:
- fields get added/removed
- meanings change
- formats evolve

So we need a way to ensure:
> old events still work with new code, and new events don’t break old consumers.