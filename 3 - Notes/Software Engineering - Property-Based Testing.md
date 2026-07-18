Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Property-Based Testing (PBT) is a testing approach where instead of writing tests for specific examples, you define general properties (rules/invariants) that must always hold, and a testing framework automatically generates many inputs to check whether those properties are true.

The main idea:
> Instead of saying "for this input, I expect this output", you say "for all valid inputs, this rule should always be true."
# Example
Instead of testing specific cases when a function should work, we define properties.

For a reverse function:
```python
def reverse(items):
    return items[::-1]
```
possible properties are:
## Property 1: Reversing twice gives the original list
For every list `x`:
```python
reverse(reverse(x)) == x
```

Examples:
```python
reverse(reverse([1,2,3]))
= reverse([3,2,1])
= [1,2,3]
```
## Property 2: Length stays the same
For every list `x`:
```python
len(reverse(x)) == len(x)
```
## Property 3: Elements stay the same
For every list `x`:
```python
set(reverse(x)) == set(x)
```

The framework then generates hundreds or thousands of random lists and checks these properties.
# Tools
- Python - Hypothesis