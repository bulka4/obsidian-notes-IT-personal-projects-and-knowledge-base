Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
The 2PC (Two-Phase Commit) is a data consistency pattern ([[Backend Engineering - Distributed microservices - Data Consistency Patterns (distributed transactions)|link]]) used in distributed microservices ([[Backend Engineering - Distributed microservices|link]]).

It makes sure that all the services have a technical ability to perform their tasks.
# How it works
When services have some actions to perform, then in 2PC method we have two phases:
## 1. Prepare phase
All services check whether they are able to perform some action, whether they have a technical ability to do this. 

They check it for example by:
- acquiring necessary database locks
- validating constraints (e.g. foreign keys, uniqueness)
- writing changes to its transaction log (WAL) so they can survive a crash
- keeping the transaction open without committing

They don't check it by checking business logic, for example:
- Is the user allowed
- Does the customer have enough money
## 1. Commit phase
Coordinator tells everyone to commit (perform their action).
# Pros:
- Strong consistency (ACID-like)
- All-or-nothing guarantee
# Cons:
- Blocking (can freeze if coordinator fails)
- Very slow in distributed systems
- Poor scalability
- Rarely used in modern microservices