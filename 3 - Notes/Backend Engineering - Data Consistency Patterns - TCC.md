Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
The TCC (Try-Confirm-Cancel) is a data consistency pattern ([[Backend Engineering - Distributed systems - Data Consistency Patterns (distributed transactions)|link]]) used in distributed microservices ([[Backend Engineering - Distributed systems|link]]).

It is used when services requires some resources to complete their action. It is about logical resources needed for a logical action, not technical ability.

In this method we check whether all the required logical resources are available to perform some logical action.

For example:
- We CAN use it in a banking application, where we check whether a user has enough money on their account to withdraw money
- We CAN NOT use it in a application, where we check whether a service is able to connect to a database (this is a technical ability to do something, not a logical resource needed for a logical operation)
# How it works
Each operation has 3 phases:
- Try → reserve resources needed to complete service's action
- Confirm → commit permanently (service performs some action using reserved resources)
- Cancel → rollback reservation (restore reserved resources to available state)

The cancel step can be performed only after the try step, not after the confirm.

Example:
- Try: reserve money
- Confirm: deduct money
- Cancel: release reservation
# Pros:
- more predictable than Saga
- avoids some inconsistencies
- good for payments/reservations
# Cons:
- complex to implement
- requires business logic changes everywhere