Tags: [[_Python]]

# General notes about async programming
General notes about async programming, not just for Python - [[Software Engineering - Async programming models]].

It is a good introduction before reading notes here for Python specifically.
# Coroutine object
When we call a coroutine ([[Software Engineering - Async programming models - Coroutines & tasks|link]]), it returns a coroutine object:
```python
async def task():
    do_step_1()
    await something()
    do_step_2()
    
obj = task() # obj is a coroutine object
```

When we create a coroutine object `obj = task()`, we don't run any computation yet. It is an object that only represents computations to perform.
# Executing a coroutine (running computations) using `await` command
To execute a coroutine (run computations), we need to use the `await` command. We can run a coroutine and get the result immediately:
```python
result = await task() # run a coroutine and get the result immediately
```

or we can first create a coroutine object and run it later:
```python
cor_obj = task() # create a coroutine object, dont run any computations yet
result = await cor_obj # run coroutine's computations and get the result
```

The `await` command can be used only inside of an asynchronous function and together with an asynchronous function (we can't run `await normal_function()` using a normal function which is not a coroutine).
# Event loop
We can create an event loop ([[Software Engineering - Async programming models - Event loops|link]]) using for example the `asyncio.run()` function like this:
```python
import asyncio

# async function (coroutine)
async def task1(x):
	await asyncio.sleep(x)
	print(f'task (x) done')
	
async def task2():
	# run tasks one by one
	await task1(1)
	await task1(2)
	
async def task3():
	# run tasks concurently
	t1 = task1(1) # coroutine object, not running yet
	t2 = task1(2)
	
	await asyncio.gather(t1, t2)
	
# Run one event loop - for running tasks one by one
asyncio.run(task2())

# Run another event loop - for running tasks concurrently.
# This loop will run once the previous one is finished
asynction.run(task3())
```
## `FastAPI`
`FastAPI` creates an event loop for use so we can use asynchronous functions.