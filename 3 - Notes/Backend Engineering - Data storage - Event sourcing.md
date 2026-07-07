Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Event Sourcing is a persistence pattern used in data storage where we store every change as an immutable event instead of storing only the current state.

For example, instead of only storing the current balance of a back account, in this approach we store events like:
```
- AccountCreated(balance=1000)
- MoneyDeposited(amount=300)
- MoneyWithdrawn(amount=100)
- MoneyDeposited(amount=200)
```

and to get the current balance (current state), we replay events:
```
1000
+300
-100
+200
------
1400
```
# Relates topics
Related topics:
- Event schema evolution - [[Backend Engineering - Data storage - Event schema evolution|link]] 
- Event replay - [[Backend Engineering - Data storage - Event replay|link]] 