Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
State machine testing is a testing technique where we test things like:
- **State behavior** — does the system behave correctly while in a particular state?
- **State transitions** — does the correct event/action move the system to the correct next state?
- **Invalid transitions** — does the system correctly reject transitions that shouldn't be possible?
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
- Depositing money changes the state correctly (amount of money in an account).
- After unfreezing, normal operations resume, they work correctly again.
# Why is it useful?
Many systems are not just functions:
```python
result = function(input)
```

They have history and memory:
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

A bug might only appear after a sequence of operations:
```
connect()
send_request()
timeout()
retry()
close()
send_request()
```

State machine testing generates and checks these sequences.