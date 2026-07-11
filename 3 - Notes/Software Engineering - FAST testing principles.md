Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The FAST testing principles are guidelines for writing good automated tests.

**FAST** is an acronym:
```
F - Fast
A - Autonomous
S - Simple
T - Thorough
```
# Fast
Tests should run quickly because tests are run frequently.
# Autonomous
Tests should run independently.

A test should not depend on:
- another test running before it
- shared data
- external services
- a developer's machine state
# Simple
Tests should be easy to understand and maintain.

A test should clearly show:
- what is being tested
- what input is used
- what result is expected
# Thorough
Tests should cover important behavior.

This does not mean:
> Test every line of code.

It means testing:
- normal cases
- edge cases
- failure cases
- important business rules