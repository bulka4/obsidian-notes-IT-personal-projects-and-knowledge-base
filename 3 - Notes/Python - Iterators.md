Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
An iterator is an object that allows you to retrieve elements one by one, typically in a loop.

In Python, an object is an iterator if it implements:
- `__iter__()` – returns the iterator itself
- `__next__()` – returns the next value or raises `StopIteration`

Example:
```python
numbers = [1, 2, 3]

it = iter(numbers)  # creates an iterator

print(next(it))  # 1
print(next(it))  # 2
print(next(it))  # 3
```

A `for` loop internally does something similar:
```python
it = iter(numbers)

while True:
    try:
        x = next(it)
        print(x)
    except StopIteration:
        break
```
# Iterable vs iterator
It is also important to distinguish:
- Iterable - An object that can create an iterator (`__iter__()`). Examples: `list`, `tuple`, `dict`, `set`, `str`.
- Iterator - The object that actually keeps track of the current position and returns elements one by one (`__next__()`).
# Generators
Generators are a special kind of iterator:
```python
gen = (x*x for x in range(3))
```

`gen` is already an iterator, so:
```python
iter(gen) is gen   # True
```

whereas:
```python
numbers = [1,2,3]
iter(numbers) is numbers   # False
```