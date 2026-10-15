Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Functional concurrency is an approach to concurrency ([[Software Engineering - Concurrency|link]]) that uses functional programming principles to make parallel and concurrent code safer.

It is about avoiding having multiple functions updating a shared, mutable data and instead making those functions operating on separate, independent data / variables.
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