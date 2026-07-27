Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Lazy evaluation means that a computation is not executed immediately when it is defined. It is executed only when the result is actually needed.
# Example
## Simple example
For example, in eager evaluation (the opposite to lazy):
```python
id = "example"

result = expensive_calculation()
print("Done")
```
`expensive_calculation()` runs immediately, even if `result` is never used.

In lazy evaluation:
```python
result = lazy(expensive_calculation)

# nothing happens yet

value = result.get()
# now expensive_calculation() runs
```

The computation is delayed until `get()` is called.
## Python generators
Python generators ([[Python - Generators|link]]) are example of a lazy evaluation because when we create an iterator:
```python
def numbers():
    for i in range(1000000):
        yield i

nums = numbers()
```

no million numbers are created, computation is paused.
## Other examples
- SQL queries (database decides when/how to execute)
- Spark RDD/DataFrame operations (transformations are lazy; actions trigger execution)
- LINQ in .NET
# Why is it useful
## 1. Memory efficiency
Instead of loading everything:
```python
data = load_all_rows_from_database()
```

you process rows one by one:
```python
for row in stream_rows():
    process(row)
```
## 2. Avoid unnecessary work
Example:
```python
query = database.query(...)
```

The database may not execute until you actually consume the results.
## 3. Build processing pipelines
Example:
```python
data = (
    read_file()
    .filter(...)
    .map(...)
)
```

The operations can be stored and executed later as one optimized pipeline.