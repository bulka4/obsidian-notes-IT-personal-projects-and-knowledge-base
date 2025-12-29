Tags: [[__Machine_Learning_Engineering]]

# Introduction
Actor is created based on a Python class. It is a logical object where we have defined calculations.

To every actor there is assigned a worker process which will be executing the code when calling actor’s methods.

Actors are stateful, they contain a state, which are class attributes.

For example if our actor is created based on such a class:
```python
import ray

ray.init() # Start Ray

@ray.remote
class Counter:
	def __init__(self):
		self.value = 0
		
	def increment(self):
		self.value += 1
		return self.value
		
# Create an actor
counter_actor = Counter.remote()

# Call methods
print(ray.get(counter_actor.increment.remote())) # 1
print(ray.get(counter_actor.increment.remote())) # 2
```

Then self.value is this actor’s state.

We can call actor’s methods multiple times during their life and their state is preserved between calls.
# Asynchronous methods call
More information about asynchronous methods call we can find here - [[Ray Core Actors - Asynchronous methods call]].
# Processes communication and workflow
More information about processes communication and workflow we can find here - [[Ray Core Actors - Processes communication and workflow]].

#MLEngineering 