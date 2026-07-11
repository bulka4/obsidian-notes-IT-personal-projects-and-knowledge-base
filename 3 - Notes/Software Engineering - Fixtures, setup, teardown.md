Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Fixtures / setup / teardown are mechanisms for preparing and cleaning up the environment around tests.

They avoid repeating the same preparation code in every test.
# Setup (Arrange)
Code that runs **before a test**.

Example:
```
Setup:
  Create test database
  Insert test user

Run test
```
# Teardown (Cleanup)
Code that runs after a test.

Example:
```
Run test

Teardown:
  Delete test database
  Remove test files
```
# Fixture
A fixture is a reusable object/environment provided to tests.

Example:
```python
@pytest.fixture
def user():
    return User("Alice")

def test_user_name(user):
    assert user.name == "Alice"
```

The fixture creates the `user` object and provides it to the test.
## Fixture scopes
Common fixture scopes:
- **per test** → create fresh data for every test
- **per class** → shared within a group of tests
- **per module** → shared across a file
- **global** → once for the whole test suite
# Why use them?
- avoid duplicated setup code
- ensure consistent test environments
- make tests cleaner
- improve test isolation