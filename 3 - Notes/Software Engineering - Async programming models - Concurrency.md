Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Using asynchronous programming, we can achieve concurrency ([[Software Engineering - Concurrency|link]]), i.e. to allow to:
- start multiple tasks
- progress on one task at a time
- when one task can't progress further because it waits for something (e.g. it can wait for retrieving data from a database), then start progressing on another task

The general pattern is:
- Create an asynchronous operation
- Create an object (e.g. handle / future / promise / task) representing it
- Start executing all operations in a concurrent mode (i.e. progress with one operation at a time and when one operation is waiting for something then another operation can be progressed)
- Wait for all operations to finish

Code looks usually like this:
```
task_a = start_async(A)
task_b = start_async(B)

results = wait_for_all(task_a, task_b)
```

When we create an object representing an operation:
```
task_a = start_async(A)
```
then this operation can be started immediately or it can be started later, when we run:
```
results = wait_for_all(task_a, task_b)
```

It depends on the tool we use.