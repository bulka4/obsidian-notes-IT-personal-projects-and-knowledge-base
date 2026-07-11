Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Table-driven tests are a way of writing tests where we store test cases as a table of inputs and expected outputs, then run the same test logic for every row.

They are similar to parameterized tests.
# Example
Without table-driven tests:
```python
def test_add_positive():
    assert add(2, 3) == 5

def test_add_zero():
    assert add(0, 3) == 3

def test_add_negative():
    assert add(-2, 3) == 1
```

With a table:
```python
test_cases = [
    (2, 3, 5),
    (0, 3, 3),
    (-2, 3, 1)
]

for a, b, expected in test_cases:
    assert add(a, b) == expected
```

The table contains:
```
Input A | Input B | Expected result
-----------------------------------
2       | 3       | 5
0       | 3       | 3
-2      | 3       | 1
```
# Why use them?
## 1. Less duplicated code
Instead of many almost identical tests, you have one test with many cases.
## 2. Easy to add new cases
Add another row:
```
100 | 200 | 300
```

No new test code needed.
## 3. Clear overview of scenarios
Example:
```
Login tests:

username | password | expected
--------------------------------
alice    | correct  | success
alice    | wrong    | failure
empty    | empty    | failure
```

The test cases become easy to review.
# Common use cases
Especially useful for:
- validation logic
- parsers
- algorithms
- edge cases
- API input testing
- mathematical functions

Example for a database parser:
```
SQL input              Expected
--------------------------------
SELECT * FROM users    Valid
SELECT                 Invalid
DROP TABLE users       Rejected
```
