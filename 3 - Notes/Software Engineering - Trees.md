Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A **tree** is a data structure that organizes data in a **hierarchical structure** made of **nodes connected by edges**.

Example:
```
          A
        /   \
       B     C
      / \     \
     D   E     F
```

Terms:
- **Root** → top node (`A`)
- **Parent** → node with children (`B` is parent of `D`)
- **Child** → node below another node
- **Leaf** → node without children (`D`, `E`, `F`)
# Binary Tree
A tree where each node has at most two children:
```
       10
      /  \
     5    20
```
# Binary Search Tree (BST)
A binary tree with ordering:
```
Left child < Parent < Right child
```

Example:
```
        10
       /  \
      5    20
     / \     \
    2   7     30
```

Searching:
1. Start at root.
2. Go left if smaller.
3. Go right if larger.

Average complexity:

|Operation|Complexity|
|---|---|
|Search|O(log n)|
|Insert|O(log n)|
|Delete|O(log n)|

However, an unbalanced tree can become:
```
10
 \
 20
   \
    30
```

Then operations become:
```
O(n)
```
# Balanced trees
To avoid degeneration, systems use balanced trees:
## AVL tree
- Strictly keeps height balanced.
- Faster lookups.
- More expensive updates.
## Red-Black tree
- Less strict balancing.
- Common in standard libraries.

Example:
- C++ `std::map`
- Java `TreeMap`
# B-Trees
Very important in databases.

Unlike binary trees, nodes can have many children:
```
          [50 | 100]
        /     |      \
    [10]   [70]   [120]
```

Advantages:
- optimized for disk access
- fewer disk reads

Used in:
- databases
- filesystems

Examples:
- PostgreSQL indexes
- MySQL InnoDB indexes
- many filesystem structures
# Trie (prefix tree)
Used for strings:
```
        root
        |
        c
        |
        a
       / \
      t   r
```

Used for:
- autocomplete
- dictionaries
- search suggestions
## Tree vs Hash Table

| |Tree|Hash table|
|---|---|---|
|Lookup|O(log n)|O(1) average|
|Ordered data|✅|❌|
|Range queries|✅|❌|
|Exact key lookup|Good|Excellent|
## Example
Find all users:
```
age between 20 and 30
```

A tree index is useful.

Find:
```
user_id = 12345
```

A hash table is often better.
## Why trees matter in backend engineering
Trees appear everywhere:
- **Databases**
    - B-tree indexes
    - query optimization
- **Filesystems**
    - directories are trees
- **Compilers**
    - Abstract Syntax Trees (ASTs)
- **Networking**
    - routing trees
- **Distributed systems**
    - hierarchical metadata structures

A good mental model:
```
Array        → access by position
Hash table   → fast lookup by key
Tree         → ordered hierarchy and efficient searching
Graph        → arbitrary relationships
```

For backend/data engineering, B-trees and tree-based indexes are especially important, because databases rely heavily on them.