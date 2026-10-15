Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Fixtures / setup / teardown are mechanisms for preparing and cleaning up the environment around tests. Both can use fixtures ([[Software Engineering - Fixtures|link]]) for that.

They avoid repeating the same preparation code in every test.
# Setup (Arrange)
Code that runs before a test. Preparing an environment for running tests. It uses fixtures ([[Software Engineering - Fixtures|link]]).

Example:
```
Setup:
  Create test database
  Insert test user

Run test
```
# Teardown (Cleanup)
Code that runs after a test. Cleaning up an environment for running tests. It can use fixtures ([[Software Engineering - Fixtures|link]]).

Example:
```
Run test

Teardown:
  Delete test database
  Remove test files
```
# Why use them?
- avoid duplicated setup code
- ensure consistent test environments
- make tests cleaner
- improve test isolation