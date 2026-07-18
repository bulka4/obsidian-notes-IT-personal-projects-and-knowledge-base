Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
Python generators are a way to create iterators ([[Python - Iterators|link]]) that produce values lazily, meaning they generate items one at a time instead of storing everything in memory.
# How to create a generator using `yield`
A generator is usually created using the `yield` keyword:
```python
def count_up_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1
```

Usage:
```python
gen = count_up_to(3)

for x in gen:
    print(x)
```
## How `yield` works
When `yield` is reached:
1. The current value is returned.
2. The function's state (local variables, execution position) is saved.
3. On the next iteration, execution resumes right after `yield`.
# Advantages
- **Memory efficient** – useful for large datasets or infinite sequences.
- **Can represent streams of data** – e.g., reading large files line by line.
- **Allows pipelined processing**.
# Example of an infinite generator
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b
```
# Generator expressions
Generators can also be written similarly to list comprehensions:
```
squares = (x * x for x in range(1000000))
```

This does not create a million-element list in memory. Values are computed only when requested.
# Internally
A generator implements the iterator protocol (`__iter__()` and `__next__()`), so:
```python
gen = count_up_to(3)

next(gen)  # 1
next(gen)  # 2
next(gen)  # 3
```

After all values are produced, `next()` raises `StopIteration`.