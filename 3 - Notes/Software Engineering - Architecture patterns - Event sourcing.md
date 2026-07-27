Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Event Sourcing is a way of modeling state where the source of truth is a sequence of events (state is a result of applying all the events). 

We store every change as an immutable event instead of storing only the current state. 

It is commonly used in databases.
# Example
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
# Properties of events
Events are:
- **Immutable** (never modified)
- **Ordered** (their order matters)
- **Represent facts that happened in the past**
# Projections
Events can be used to build different projections (views) of a state, for example:

Events:
```
MoneyDeposited(300)
MoneyWithdrawn(100)
MoneyDeposited(200)
```

Projection 1:
```
Current balance = 1400
```

Projection 2:
```
Total deposited = 500
```

Projection 3:
```
Transaction history page
```
# Snapshots
- Snapshot is a saved state at a specific point in time. 
- We can create snapshots once in a while to have information about the recent state
- When we want to know the current state, we check the latest snapshots and apply events that happened after it, so we don't need to recalculate the state from scratch (by applying all the events) every time (which is costly if there is a lot of events).
# Fixing invalid events
If we encounter some invalid / incorrect events that need to be fixed, usually we don't change them but create another compensating event which makes a fix.

For example, if we subtracted incorrectly money from a bank account, we can create a new event which adds new money, the same amount.
# Event schema evolution (changing events)
We shouldn't be updating / deleting events but we need to modify them when their schema changes (data types, available fields). This is so called event schema evolution ([[Software Engineering - Event sourcing - Event schema evolution|link]]).
# Event replay
Event replay ([[Software Engineering - Event sourcing - Event replay|link]]) is used to reprocesses events, recover consumers, build new projections, debug, etc.
# How to implement it
## 1. Define events
Events are immutable objects representing things that happened.
```python
class AccountCreated:
    def __init__(self, initial_balance):
        self.initial_balance = initial_balance

class MoneyDeposited:
    def __init__(self, amount):
        self.amount = amount

class MoneyWithdrawn:
    def __init__(self, amount):
        self.amount = amount
```
## 2. Create an event store
The event store stores events.

A simple in-memory version:
```python
class EventStore:
    def __init__(self):
        self.events = []

    def append(self, event):
        self.events.append(event)

    def get_events(self):
        return self.events
```

In production, this could be:
- PostgreSQL table
- dedicated event store
- Kafka log

Example table:
```
events
------------------------------------------------
id | aggregate_id | event_type | data
------------------------------------------------
1  | 123          | AccountCreated | {"balance":1000}
2  | 123          | MoneyDeposited | {"amount":300}
```
## 3. Create an event-sourced entity
The entity does not store only the current state permanently.

Instead, it:
- applies events to update its state
- creates new events when something happens
```python
class BankAccount:
    def __init__(self):
        self.balance = 0

    def apply(self, event):
        if isinstance(event, AccountCreated):
            self.balance = event.initial_balance

        elif isinstance(event, MoneyDeposited):
            self.balance += event.amount

        elif isinstance(event, MoneyWithdrawn):
            self.balance -= event.amount

    def deposit(self, amount):
        if amount <= 0:
            raise Exception(
                "Invalid amount"
            )

        event = MoneyDeposited(amount)
        self.apply(event)

        return event

    def withdraw(self, amount):
        if amount > self.balance:
            raise Exception(
                "Insufficient funds"
            )

        event = MoneyWithdrawn(amount)
        self.apply(event)

        return event
```

Notice:
```python
event = MoneyDeposited(amount)
```

The operation creates an event.

The event becomes the permanent record.
## 4. Reconstruct the account from events
When loading an account:
```python
def load_account(events):
    account = BankAccount()

    for event in events:
        account.apply(event)

    return account
```

Example:

Events:
```
AccountCreated(1000)
MoneyDeposited(300)
MoneyWithdrawn(100)
```

Replay:
```
1000
+300
-100
----
1200
```

Current object:
```
account.balance
# 1200
```
## 5. Application use case
The use case ([[Software Engineering - Architecture concepts - Use case|link]]) coordinates everything.

Example:
```python
class DepositMoneyUseCase:
    def __init__(
        self,
        event_store
    ):
        self.event_store = event_store

    def execute(
        self,
        account_id,
        amount
    ):
	    # Get all the events so far for the account
        events = (
            self.event_store
            .get_events(account_id)
        )
        # apply all the events from the past (add or remove money for each event)
        account = load_account(events)
        # create a new event for deposit
        new_event = account.deposit(amount)

		# Save info about the new event
        self.event_store.append(
            new_event
        )
```

Flow:
```
User requests deposit
          |
          v
Use case
          |
          v
Load previous events
          |
          v
Rebuild Account object
          |
          v
Call account.deposit()
          |
          v
Create MoneyDeposited event
          |
          v
Save event
```
# Benefits
- It gives us a complete history
- Allows for time travel - we can reconstruct a state at any point in time
- Auditing - we can check what events happened to explain issues
- Building projections
# Drawbacks
- Reading can be expensive - if we need to reconstruct a state by applying all the events
- Events can't be easily changed - we shouldn't be modifying events but create another compensating events instead