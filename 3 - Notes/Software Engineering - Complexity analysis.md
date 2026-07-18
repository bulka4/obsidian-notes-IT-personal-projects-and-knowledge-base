Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Complexity analysis is the process of analyzing how much **time** and **memory** an algorithm requires as the input size grows.

It helps answer:
> "How does this algorithm scale?"
# Big-O notation
Complexity is usually expressed using Big-O notation:
```
O(f(n))
```

It describes the growth rate, ignoring constants.

Example:
```
for i in range(1000):
    print(i)
```

Technically:
```
O(1000)
```

but we simplify:
```
O(1)
```

because the amount of work does not grow with `n`.
# Types
## 1. Time complexity
How the **execution time** grows with input size `n`.

Examples:
```
O(1)       → constant time
```

Example: accessing an array element by index.
```
O(n)       → linear time
```

Example: searching through every element in a list.
```
O(n²)      → quadratic time
```

Example: comparing every pair of elements.
```
O(log n)   → logarithmic time
```

Example: binary search.
## 2. Space complexity
How much additional memory an algorithm uses.

Example:
```
new_list = []
for item in data:
    new_list.append(item)
```

Requires extra memory → `O(n)` space.