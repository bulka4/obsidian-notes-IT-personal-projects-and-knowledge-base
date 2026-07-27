Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Functional concurrency is an approach to concurrency ([[Software Engineering - Concurrency|link]]) that uses functional programming principles to make parallel and concurrent code safer.

The main idea is:
> Avoid shared mutable state ([[Backend Engineering - Distributed systems - State|link]]). Instead, use immutable data and independent computations that can run safely at the same time.
# Traditional concurrent code
```python
id = 0

def add():
    global id
    id += 1
```

If multiple threads run `add()` simultaneously, they modify the same state and you need locks ([[Software Engineering - Concurrency - Locks|link]]):
```python
lock.acquire()
id += 1
lock.release()
```
# Functional approach
```python
def add(value):
    return value + 1
```

Each function:
- receives input,
- produces output,
- does not modify shared data.

So multiple calls can run independently:
```python
add(1)  → 2
add(5)  → 6
add(10) → 11
```

No locks are needed.