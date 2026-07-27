Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
In async programming ([[Software Engineering - Async programming models|link]]):
- **Tasks** are operations that can be paused and resumed later
- **Coroutines** are functions defining those tasks

When a coroutine pauses (e.g. because it waits to load data from a database), another coroutine within the same event loop ([[Software Engineering - Async programming models - Event loops|link]]) can progress with its tasks.
# Example
A coroutine can be for example a function in Python like this:
```python
async def task():
    do_step_1()
    await something()
    do_step_2()
```

This coroutine:
- Can pause at: `await something()`
- While it waits for the `something()` to finish, another coroutine can be started 
- Later the `task` coroutine can continue from the `await` point
# Switching between coroutines
The flow of switching between coroutines (starting another coroutine when one is waiting) looks like this:
- Coroutine A starts
- It reaches a point where it waits for something (we use `await`)
- Then, another coroutine B can be started while A is waiting
- Coroutine B runs until it is finished or it also reaches a point where it waits for something (i.e. it reached `await` point)
- If coroutine B is finished or is waiting and A already finished waiting, then A is resumed.
# What a coroutine returns
When we run a coroutine, it doesn't return the actual result of a function but some object which:
- Represents operations to perform
- In some languages it runs immediately, in others it doesn't and we can specify later when to run it
- Once operations are completed, we can use this object to get the result of those operations (returned value)

Those are different objects in different programming languages:
- JavaScript → Promise
- Python (`asyncio`) → Future
- C# → Task (similar idea)
- Java → Future / CompletableFuture
## Example
For example, in Python, if we run a coroutine like this:
```python
async def task():
	return 5
	
x = task()
```

then the `x` variable is not the result 5 but it is an object which represents computations to perform.

We can run computations for this object later and get a result:
```python
x = task()
result = await x # execution starts here
```

When we run `await x` then computations starts and the `result` variable contains the returned value 5.