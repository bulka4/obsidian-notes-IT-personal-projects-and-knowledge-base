Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A race condition occurs when multiple concurrent operations access and modify shared data, and the final result depends on the timing or order in which those operations execute.

Example:
```
Initial balance = $100

Thread A: withdraw $80
Thread B: withdraw $50
```

Both threads read:
```
balance = $100
```

Then:
```
Thread A calculates: 100 - 80 = 20
Thread B calculates: 100 - 50 = 50
```

If Thread B writes last:
```
Final balance = $50
```

The system incorrectly allowed withdrawing $130 from a $100 account.
# How to prevent race conditions
Common techniques:
- **Locks / mutexes** → allow only one thread to access critical sections
- **Atomic operations** → operations that happen as one indivisible step
- **Immutable data** → avoid modifying shared state
- **Message passing** → avoid shared memory between components