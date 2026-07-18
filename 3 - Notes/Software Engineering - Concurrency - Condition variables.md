Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A condition variable is a synchronization primitive that allows a thread to:
1. Wait until some condition becomes true
2. Be notified by another thread when the condition may have changed

The key idea is:
> "I cannot continue now, so I'll go to sleep and let someone wake me up later."
# Example
producer-consumer queue.

Consumer:
```python
lock.acquire()

while queue.is_empty():
    condition.wait()   # sleep

item = queue.pop()

lock.release()
```

Producer:
```python
lock.acquire()

queue.push(item)
condition.notify()     # wake one waiting thread

lock.release()
```

What happens:
```
Consumer:
    queue empty -> wait() -> sleeps

Producer:
    adds item
    notify()

Consumer:
    wakes up and continues
```
# Important points
- A condition variable is always used together with a lock ([[Software Engineering - Concurrency - Locks|link]].
- `wait()` usually:
    1. Releases the lock.
    2. Puts the thread to sleep.
    3. Re-acquires the lock when the thread wakes up.
## Why release the lock?
Because otherwise the producer could never acquire the lock to add data and wake the consumer.

A condition variable does not store the condition itself.
# Typical uses
- Producer-consumer queues
- Waiting for tasks to complete
- Thread pools
- Waiting for resources to become available