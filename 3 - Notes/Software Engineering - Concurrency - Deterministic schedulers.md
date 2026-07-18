Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Deterministic schedulers are schedulers that control the order in which concurrent tasks ([[Software Engineering - Concurrency|link]]) (threads, processes, goroutines, etc.) are executed so that the same execution order can be reproduced repeatedly.

Normally, a scheduler is unpredictable:
```
Run 1:
Thread A → Thread B → Thread A

Run 2:
Thread B → Thread A → Thread A
```

This makes concurrency bugs ([[Software Engineering - Concurrency - Synchronization bugs|link]]) (like race conditions) difficult to reproduce.

A deterministic scheduler can force:
```
Every run:
Thread A → Thread B → Thread A
```

so a bug appears consistently and can be debugged.

Example:
```
Thread A:
    balance = balance - 100

Thread B:
    balance = balance + 50
```

A normal scheduler might execute them in different orders each time. A deterministic scheduler can deliberately choose an order that exposes the bug.