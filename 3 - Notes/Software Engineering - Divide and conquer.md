Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Divide and conquer** is an algorithmic strategy where you solve a problem by:
1. **Divide** → split the problem into smaller subproblems.
2. **Conquer** → solve the smaller problems (often recursively).
3. **Combine** → merge the solutions into the final answer.

General pattern:
```
Large problem
      |
      ↓
Split into smaller problems
      |
      ↓
Solve smaller problems
      |
      ↓
Combine results
```
# Example: Merge sort
Sorting:
```
[8, 3, 5, 1]
```

Divide:
```
[8,3]     [5,1]
```

Divide again:
```
[8] [3]   [5] [1]
```

Conquer:
```
[3,8]     [1,5]
```

Combine:
```
[1,3,5,8]
```

Complexity:
```
O(n log n)
```
## Example: Binary search
Find a value in a sorted array:
```
[1,3,5,7,9,11,13]
```

Check middle:
```
        7
```

If target is larger:
```
ignore left half
```

Repeat on the remaining half.

Complexity:
```
O(log n)
```
# Why it is useful
Many problems become easier when broken into independent smaller pieces.

Advantages:
- reduces complexity
- enables parallel processing
- often produces elegant recursive solutions
# Common examples

|Algorithm|Divide and conquer idea|
|---|---|
|Merge sort|Split array, sort halves, merge|
|Quick sort|Partition around pivot|
|Binary search|Eliminate half the search space|
|FFT|Split signal into smaller parts|
# Relation to other patterns
```
Divide and conquer
        |
        ├── Recursive decomposition
        ├── Merge sort
        ├── Binary search
        └── Quick sort


Dynamic programming
        |
        └── Divide into overlapping subproblems + remember results


Greedy
        |
        └── Make best local choice without exploring all options
```
A key distinction:
- **Divide and conquer** → subproblems are usually **independent**.
- **Dynamic programming** → subproblems often **overlap**, so we cache results.

For backend/data engineering, divide and conquer appears in:
- distributed computing (MapReduce: split data → process chunks → combine results)
- Spark jobs (partition data → process partitions → aggregate)
- parallel algorithms
- database query execution.