Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Backtracking** is an algorithmic technique where you **build a solution step by step, and if a choice leads to a dead end, you undo it and try another choice**.

The idea:
> Try a possibility → check if it works → if not, go back and try a different path.

It is essentially a **systematic search through possible solutions**.
# Basic pattern
```
Choose
  ↓
Explore
  ↓
If invalid → undo choice (backtrack)
  ↓
Try another choice
```

Example:
```
          Start
        /   |   \
       A    B    C
      / \
     ...
```

The algorithm explores paths and abandons impossible ones.
# Example: Maze solving
Imagine a maze:
```
Start → → → ?
          |
          X (dead end)
```

Process:
1. Move forward.
2. Hit dead end.
3. Go back.
4. Try another direction.
# Example: Generating combinations
Find all subsets of:
```
[1, 2, 3]
```

Decision tree:
```
          []
        /    \
      [1]     []
     /  \     / \
 [1,2] [1]  [2] []
```

Backtracking explores all valid possibilities.
# Classic problems

## 1. N-Queens
Place `N` queens on a chessboard so none attack each other.

Example:
```
Q . .
. . Q
. Q .
```

Algorithm:
- place a queen
- check validity
- if conflict → remove queen
- try another position
## 2. Sudoku solver
Steps:
1. Choose an empty cell.
2. Try a number.
3. Check rules.
4. Continue.
5. Undo if impossible.
## 3. Path finding
Find possible paths through a graph or grid.
# Complexity
Backtracking is often expensive because it explores many possibilities.

Example:

Generating all subsets:
```
n elements → 2ⁿ possible subsets
```

Complexity:
```
O(2ⁿ)
```

However, **pruning** can make it much faster.

Example:
```
Without pruning:
Explore every possibility

With pruning:
Stop early when a path cannot work
```
# Backtracking vs Dynamic Programming
They are related but solve different problems:

| |Backtracking|Dynamic programming|
|---|---|---|
|Goal|Find possible solutions|Optimize/count solutions|
|Approach|Explore choices|Store results|
|Reuse results|Usually no|Yes|
|Typical complexity|Exponential|Often polynomial|
Example:

**Knapsack**
- Backtracking: try every combination.
- Dynamic programming: remember best solutions for smaller capacities.
# Backtracking in software engineering
Used in:
- constraint solving
- scheduling
- configuration systems
- compilers
- AI search
- testing combinations

For example:

A deployment system might search:
```
Choose:
- server
- region
- resources

If constraints fail:
- undo choice
- try another configuration
```

# Mental model
```
Greedy:
  Choose best now

Dynamic programming:
  Remember previous solutions

Backtracking:
  Try choices and undo when wrong
```

For backend engineering, you probably won't implement backtracking daily, but understanding it helps with search problems, optimization, and constraint-based systems.