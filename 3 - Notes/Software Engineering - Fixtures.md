Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
A test fixture is an environment used to perform tests or a mechanism (e.g. a function, piece of code, configuration) used to prepare this environment (it can mean both).

A fixture can also mean a mechanism used to clean this environment (remove it).

This environment can include a database setup, data, objects (class instances), environment variables, files, network configuration.

Example:
```python
@pytest.fixture
def user():
    return User("Alice")

def test_user_name(user):
    assert user.name == "Alice"
    
user = user()
test_user_name(user)
```

The fixture creates the `user` object and provides it to the test.
# Fixture scopes
Common fixture scopes:
- **per test** → create fresh data for every test
- **per class** → shared within a group of tests
- **per module** → shared across a file
- **global** → once for the whole test suite