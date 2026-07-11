Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Test coverage measures how much of the code is executed when tests run, i.e. how much of the code is being tested.

Types of coverage:
- line coverage - how many lines were executed
- branch coverage - how many decision paths were executed (paths in `if / else` statements)
- function coverage - how many functions were called
# Limitations
## High coverage does not mean correct software
Coverage tells us how much code was tested but it doesn't tell us about how many scenarios were tested. For example, for a function:
```python
def divide(a, b):
    return a / b
```
we might run 1 test `divide(10, 2)` so we tested the entire code, but we didn't test all the possible scenarios, for example `divide(10, 0)` which fails.
## Bad tests can give high coverage
For example, for a function:
```python
def add(a, b):
    return a + b
```

such a test is bad:
```python
add(2, 3)  # no check
```
## Some code is difficult to cover
Examples:
- error handling
- rare failures
- network failures
- hardware failures
- concurrency bugs

For example:
```python
try:
    send_to_server()
except NetworkError:
    recover()
```
The recovery path may never execute during normal tests.
