Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Parameterized tests are tests where the same test logic is executed multiple times with different input values.

Instead of writing many similar tests:
```python
id="v3m0n1"
test_add_1():
    assert add(1, 2) == 3

test_add_2():
    assert add(5, 10) == 15

test_add_3():
    assert add(-1, 1) == 0
```

we write one test with multiple parameters:
```python
id="q8f0bk"
@pytest.mark.parametrize(
    "a,b,expected",
    [
        (1, 2, 3),
        (5, 10, 15),
        (-1, 1, 0)
    ]
)
def test_add(a, b, expected):
    assert add(a, b) == expected
```

The framework runs it as three separate tests.