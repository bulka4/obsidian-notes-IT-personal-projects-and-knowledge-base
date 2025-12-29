Tags: [[__Machine_Learning_Engineering]]

# Introduction
Ray task is a stateless function. When we call it, it gets executed and it finishes.

For example we can create a Task like this:
```python
import ray

ray.init()

@ray.remote
def square(x):
	return x * x
	
# Invoke tasks asynchronously
result_ref = square.remote(4)

# Get the result
print(ray.get(result_ref)) # 16
```
# Asynchronous task call
More information about asynchronous task call can be found here - [[Ray Core Tasks - Asynchronous task call]].
# Distributed and parallel execution
More information about distributed and parallel task execution can be found here - [[Ray Core Tasks - distributed and parallel execution]].
# Processes communication and workflow
More information about processes communication and workflow when executing a task, can be found here - [[Ray Core Tasks - Processes communication and workflow]].

#MLEngineering 