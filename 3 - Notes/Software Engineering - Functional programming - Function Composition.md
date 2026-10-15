Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Function composition means using an output of one function as an input for another one, for example:
```python
def double(x):
    return x * 2

def add_one(x):
    return x + 1

result = add_one(double(3))  # 7
```
# Benefits
- Build reusable processing pipelines
- Keep functions small and testable
- Avoid duplicated logic
- Common in:
    - Data processing pipelines (Spark, ETL)
    - Middleware chains
    - Request processing
    - Functional programming styles