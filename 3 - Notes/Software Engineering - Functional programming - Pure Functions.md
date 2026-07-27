Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Pure functions are functions that:
1. Always return the same output for the same input.
2. Don't depend on an external state (external state are variables outside of the function)
3. Have no side effects (they do not modify external state)
# Example
This function is impure:
```python
tax_rate = 0.23

def calculate_tax(price):
    return price * tax_rate
```

because the result depends on the external state `tax_rate` which can change.
# Benefits
- **Easier testing** — you only test input → output.
- **Easier debugging** — fewer hidden behaviors.
- **Safer parallel execution** — functions do not interfere with each other.
- **Better code reuse** — logic is independent of infrastructure.