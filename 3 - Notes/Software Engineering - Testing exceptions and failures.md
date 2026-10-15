Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Testing exceptions and failures means verifying that code behaves correctly (throws proper exceptions, handles failures correctly) when something goes wrong.

A good test should check not only the "happy path" but also error cases.
# Testing exceptions
We verify that code raises the expected error.

Example:
```python
def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b
```

Test:
```python
def test_divide_by_zero():
    with pytest.raises(ValueError):
        divide(10, 0)
```

The test passes only if the exception is raised.
# Testing exception details
Sometimes we also verify the message or error data:
```python
def test_invalid_user():
    with pytest.raises(UserNotFoundError) as error:
        find_user(123)

    assert str(error.value) == "User does not exist"
```
# Testing failures
Failures are situations where an operation cannot complete successfully.

Examples:
- invalid input
- missing file
- database unavailable
- network timeout
- permission denied

For example, we can test in a payment service what happens when someone wants to use an expired credit card.

The test verifies the whole behavior, for example:
- exception thrown
- error logged
- some earlier operations cancelled
- some operations don't succeed (e.g. no money charged)
## Important failure scenarios to test
### 1. Invalid input
```
Input:
  negative age

Expected:
  ValidationError
```
### 2. Boundary conditions
```
Maximum allowed value:
100

Test:
99   ✅
100  ✅
101  ❌
```
### 3. External dependency failures
Example:
```
Application
     |
     v
Database
```

Test:
```
Database unavailable

Expected:
- application returns error
- retries happen
- no corrupted state
```
### 4. Partial failures
Important in distributed systems.

Example:
```
Service A
    |
    v
Service B
    |
    X
failure
```

Test:
- Does A handle B failing?
- Does it retry?
- Does it return a useful error?