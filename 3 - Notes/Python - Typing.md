Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Introduction
Typing is a technique of adding type hints to variables, function parameters, and return values. For example, instead of:
```python
def add(a, b):
    return a + b
```

do:
```python
def add(a: int, b: int) -> int:
    return a + b
```
