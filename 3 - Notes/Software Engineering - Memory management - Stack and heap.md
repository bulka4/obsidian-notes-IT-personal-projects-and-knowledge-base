Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A stack and heap are memory locations with different purposes, typically:
- Stack - stores function calls, local variables data
- Heap - stores dynamically created data that can live longer (objects, large data structures).

Additionally, we have memory locations like:
- Code - stores global/static variables
- Data - stores program instructions

Example:
```
x = [1,2,3]
```

The variable `x` may be stored on the stack, while the list object is stored on the heap.