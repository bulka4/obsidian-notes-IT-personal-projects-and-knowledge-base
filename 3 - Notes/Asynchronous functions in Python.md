Tags: [[_Python]]

# Asynchronous function (coroutine)
An asynchronous function (also called coroutine) is a function which can be executed in parallel with other asynchronous functions.
# The ‘await’ command
There is also an option of executing them one by one using the ‘await’ command.

The ‘await’ command can be used only inside of an asynchronous function and together with an asynchronous function.

We can’t execute an asynchronous function without using the ‘await’ command.
# Coroutine object
We can create so called coroutine objects.

When we create a coroutine object using asynchronous function, it doesn’t run the function but we can use it later in order to run this function.
# Event loop
We can execute asynchronous functions only inside of so called event loop (explained later in this document).

We can create an event loop using for example the asyncio.run() function like this:

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

# Event loop
Event loop is like a controller for asynchronous tasks.

If we want to run an asynchronous function, it needs to run inside of an event loop.

FastAPI creates an event loop for use so we can use asynchronous functions.

Without FastAPI, we can start an event loop using for example asyncio.run().

As an argument to asyncio.run() we pass a asynchronous function we want to execute:
```python
import asyncio

async def function():
	x = function_1()
	y = await function_2()
	z = function_3()
	
asyncio.run(function())
```