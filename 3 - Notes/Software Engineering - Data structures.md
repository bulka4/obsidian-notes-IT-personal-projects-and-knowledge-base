Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Hash tables
A hash table is a data structure that stores key-value pairs and provides very fast lookup, insertion, and deletion.

It computes a hash for a key and that gives an index (a position) at which that key will be stored.

Thanks to this, the lookup is very fast because when we look for a value, we just need to calculate a hash for it and that gives us the position at which that value is stored if it exists.

More information can be found here - [[Software Engineering - Data structures - Hash tables]].
# Trees
A tree is a data structure that organizes data in a hierarchical structure made of nodes connected by edges.

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

More information can be found here - [[Software Engineering - Data structures - Trees]].
# Graphs
A graph is a data structure that represents relationships between objects. It consists of:
- Nodes (vertices) → entities
- Edges → connections between entities

More information can be found here - [[Software Engineering - Data structures - Graphs]].
# Queues
A queue is a data structure that stores elements in the "First-In, First-Out" (FIFO) order where we:
- add new elements to the end of the queue
- remove elements from the beginning of the queue

More information can be found here - [[Software Engineering - Data structures - Queues]].
# Heaps
A heap is a specialized tree-based data structure designed for quick access to the smallest or largest element.

It is usually implemented as a sorted binary tree ([[Software Engineering - Data structures - Trees|link]]) where `parent node < children` or `parent > children`.

More information can be found here - [[Software Engineering - Data structures - Heaps]].
# Related topics
1. [[Software Engineering - Data structures - Hash tables]]
2. [[Software Engineering - Data structures - Trees]]
3. [[Software Engineering - Data structures - Graphs]]
4. [[Software Engineering - Data structures - Queues]]
5. [[Software Engineering - Data structures - Heaps]]