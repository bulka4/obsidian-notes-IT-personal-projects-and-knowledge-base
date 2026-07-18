Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
Python decorators are functions used to modify or extend the behavior of another function or class without changing its code.

We can also say that decorator functions are used to insert one function A into another function B, such that when function B is executing, the function A is executed inside of it.

They are based on the fact that functions are objects, so we can pass them as arguments and return them.
# Example
```python
def logger(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@logger
def hello():
    print("Hello!")

hello()
```

Output:
```
Before function
Hello!
After function
```

So we can say that:
- The logger decorator is a function that extends the behavior of the `hello` function by adding two additional prints.
- The function that we decorate (`hello` in this case) is used inside of a decorator function
# Syntax equivalent
The syntax:
```python
@logger
def hello():
```

is equivalent to:
```python
def hello():
    ...

hello = logger(hello)
```
# Common uses
- **Logging** function calls
- **Authentication/authorization**
- **Measuring execution time**
- **Caching results**
- **Validation**
- **Framework features** (e.g., Flask routes, Django views)