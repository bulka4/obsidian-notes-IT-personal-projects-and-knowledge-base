Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Flaky tests** are tests that sometimes pass and sometimes fail without any changes to the code being tested.
# Common causes of flaky tests
## Timing issues
Example:
```
Test:
Click button
Check result immediately
```

Problem:
```
Frontend needs 2 seconds to update
Test checks after 0.1 seconds
```

Solution:
- wait for conditions
- avoid fixed sleeps
## Dependency on external systems
For example, when relying on an external API, that API may be:
- slow
- unavailable
- rate limited
## Shared state between tests
For example, test A deletes a user in a database and test B checks whether that user exists. Depending on execution order, tests can fail.
## Random data
A random value may occasionally create a failure.
