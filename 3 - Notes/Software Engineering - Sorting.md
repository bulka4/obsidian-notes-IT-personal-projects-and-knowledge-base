Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Sorting** is the process of arranging data according to some order, usually ascending or descending.

Example:
```
Before:
[5, 2, 8, 1, 3]

After:
[1, 2, 3, 5, 8]
```

Sorting is important because many algorithms become faster when data is ordered (e.g., binary search).
# Common sorting algorithms

## 1. Bubble sort
Repeatedly swaps adjacent elements if they are in the wrong order:
```
[5, 2, 3]

5 > 2 → swap

[2, 5, 3]

5 > 3 → swap

[2, 3, 5]
```

Complexity:
```
O(n²)
```

Mostly educational; rarely used in practice.
## 2. Insertion sort
Builds the sorted part one element at a time:
```
[5, 2, 3]

Take 2:
[2, 5, 3]

Take 3:
[2, 3, 5]
```

Complexity:
```
O(n²)
```

Good for:
- small datasets
- nearly sorted data
## 3. Merge sort
Divide and conquer:
1. Split array into halves.
2. Sort each half.
3. Merge them.

Example:
```
[8, 3, 5, 1]

Split:

[8,3]   [5,1]

Sort:

[3,8]   [1,5]

Merge:

[1,3,5,8]
```

Complexity:
```
O(n log n)
```

Advantages:
- predictable performance
- stable sorting
## 4. Quick sort
Choose a pivot and partition elements:
```
[5, 2, 8, 1, 3]

pivot = 5

Smaller:
[2,1,3]

Pivot:
[5]

Larger:
[8]
```

Average:
```
O(n log n)
```

Worst case:
```
O(n²)
```

Very fast in practice.
## 5. Heap sort
Uses a heap:
1. Build max-heap.
2. Repeatedly remove largest element.

Complexity:
```
O(n log n)
```
# Comparison

|Algorithm|Average|Worst|Notes|
|---|---|---|---|
|Bubble sort|O(n²)|O(n²)|Simple, slow|
|Insertion sort|O(n²)|O(n²)|Good for small data|
|Merge sort|O(n log n)|O(n log n)|Stable|
|Quick sort|O(n log n)|O(n²)|Very fast in practice|
|Heap sort|O(n log n)|O(n log n)|Good guarantees|
# Sorting in real systems
Sorting appears everywhere:
## Databases
Example:
```
SELECT *
FROM users
ORDER BY created_at;
```

The database uses sorting algorithms internally.
## Distributed systems
Large datasets cannot fit on one machine:
```
Machine A → sort chunk 1
Machine B → sort chunk 2
Machine C → sort chunk 3

        ↓

Merge sorted results
```

This is used in systems like Spark.
## Search engines
Documents may be sorted by:
- relevance score
- popularity
- date