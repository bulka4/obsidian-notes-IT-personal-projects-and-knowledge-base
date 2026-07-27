Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A callback is a function passed to another function/component that will be called later when a specific event or condition happens.

For example, in Python:
```python
def process_data(data, callback):
    result = data * 2
    callback(result)

def print_result(value):
    print(value)

process_data(5, print_result)
```
