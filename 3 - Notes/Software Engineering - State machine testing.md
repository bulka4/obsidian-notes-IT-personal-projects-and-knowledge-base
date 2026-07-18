Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**State machine testing** is a testing technique where you model a system as a **finite state machine (FSM)** and test whether it behaves correctly when moving between states through different actions/events.

The idea:
> A system has states, actions cause transitions, and tests verify that all valid and invalid transitions behave correctly.

A state machine consists of:
- **States** — the current condition of the system
- **Events/actions** — things that happen
- **Transitions** — how actions move the system from one state to another
- **Rules/invariants** — what must always be true
# Example
A bank account:
```
States:
- Empty
- Has balance
- Frozen

Events:
- deposit()
- withdraw()
- freeze()

Transitions:

Empty
  deposit()
      ↓
Has balance

Has balance
  withdraw(all money)
      ↓
Empty

Any state
  freeze()
      ↓
Frozen
```

Tests can verify:
- We cannot withdraw money from an empty account.
- A frozen account cannot accept withdrawals.
- Depositing money changes the state correctly.
- After unfreezing, normal operations resume.
# Why is it useful?
Many systems are not just functions:
```python
result = function(input)
```

They have **history and memory**:
- databases
- network protocols
- distributed systems
- user sessions
- authentication systems
- workflows
- message queues

For example, an HTTP connection:
```
CLOSED
  connect()
      ↓
CONNECTED
  send_request()
      ↓
WAITING_RESPONSE
  receive_response()
      ↓
CONNECTED
  close()
      ↓
CLOSED
```

A bug might only appear after a sequence:
```
connect()
send_request()
timeout()
retry()
close()
send_request()
```

State machine testing generates and checks these sequences.