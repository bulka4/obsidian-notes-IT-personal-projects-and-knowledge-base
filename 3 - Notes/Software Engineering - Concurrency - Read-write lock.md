Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A read-write lock is a type of lock ([[Software Engineering - Concurrency - Locks|link]]) that allows multiple threads ([[Software Engineering - Threads|link]]) to read a resource at the same time, but allows only one thread to write to it at a time.

The idea:
- Reading usually does not change data, so multiple readers can safely run together.
- Writing changes data, so it needs exclusive access.
# Example
```python
rw_lock.acquire_read()

# read data
print(user_profile)

rw_lock.release_read()
```

Multiple threads can do this:
```
Thread A: read user profile
Thread B: read user profile
Thread C: read user profile
```

All can run at the same time.

But writing requires a write lock:
```python
rw_lock.acquire_write()

# modify data
user_profile.name = "John"

rw_lock.release_write()
```

During the write:
```
Thread A: write user profile
          |
          v
     no other readers or writers allowed
```