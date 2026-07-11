Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A unit test framework is a library/tool that helps us write, organize, and run unit tests.

a test framework provides:
- test discovery
- assertions
- setup/teardown
- test organization
- reporting
- integration with IDEs and CI/CD
# Main components of a unit test framework
## Test runner
Responsible for finding and executing tests.
## Assertions
Assertions are functions that check whether the result is correct, for example:
```
assertEqual(a, b)
assertTrue(condition)
assertFalse(condition)
assertNull(value)
assertThrows(exception)
```
## Test fixtures
Code that prepares and cleans up tests.

Example:
```
Before each test:
    Create database

Run test

After each test:
    Delete database
```

Used for:
- creating objects
- initializing resources
- cleanup
## Test organization
Frameworks help group tests.

Example:
```
UserServiceTests
    ├── test_create_user
    ├── test_delete_user
    └── test_login
```

Usually through:
- test classes
- test suites
- tags/categories
# Popular frameworks
- Python - pytest
- JavaScript - Jest, Mocha, Vitest