Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Searching is the process of finding a specific element in a collection of data.

The choice of search algorithm depends on the **data structure** and whether the data is ordered.
# 1. Linear search
Check elements one by one:
```
[5, 8, 2, 10, 7]

Find 10:

5 → 8 → 2 → 10 ✓
```

Complexity:
```
O(n)
```

Works on:
- arrays
- unsorted lists
# 2. Binary search
Requires **sorted data**.

Idea:
1. Look at the middle element.
2. If target is smaller, search left half.
3. If target is larger, search right half.

Example:
```
[1, 3, 5, 7, 9, 11, 13]

Find 11:

middle = 7
11 > 7 → search right

[9, 11, 13]

middle = 11 ✓
```

Complexity:
```
O(log n)
```

Works on:
- sorted arrays
- balanced search trees
# 3. Hash table lookup
Use a hash function on the input value and output is location of that input value saved in some data structure, for example:
- In a table - Hash output is a row number
- In a list - Hash output is a position in a list

Average complexity:
```
O(1)
```

Works for:
- dictionaries
- maps
- caches
# 4. Tree search
In a Binary Search Tree:
```
        10
       /  \
      5    20
```

Search:
- smaller → go left
- larger → go right

Average:
```
O(log n)
```

Balanced trees guarantee:
```
O(log n)
```
# 5. Graph search
For graphs, common algorithms are:
## Breadth-First Search (BFS)
Search level by level:
```
A
├── B
├── C
    └── D
```

Useful for:
- shortest path in unweighted graphs
- finding connections

Complexity:
```
O(V + E)
```
## Depth-First Search (DFS)
Explore deeply:
```
A → B → C
```

Useful for:
- cycle detection
- dependency analysis

Complexity:
```
O(V + E)
```
# Summary

|Data structure|Typical search|
|---|---|
|Unsorted array/list|Linear search O(n)|
|Sorted array|Binary search O(log n)|
|Hash table|Hash lookup O(1) average|
|Balanced tree|Tree search O(log n)|
|Graph|BFS/DFS O(V+E)|

For backend engineering, searching is everywhere:
- databases use indexes (often B-trees or hash indexes)
- caches use hash tables
- search engines use inverted indexes
- distributed systems use routing/search algorithms

A good rule:
```
Need exact key lookup → Hash table
Need sorted/range queries → Tree
Need explore relationships → Graph search
Need search in sorted data → Binary search
```