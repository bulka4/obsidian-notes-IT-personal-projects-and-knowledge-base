Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
CRDTs (Conflict-free Replicated Data Types) is a method of conflict resolution ([[Backend Engineering - Distributed systems - Conflict resolution|link]]). It designs data structures so that replicas can merge automatically without conflicts or inaccuracies.
# Example
For example, if we would like to count likes received from different users, we could have data in two replicas like:
```
Replica A:
likes = 1

Replica B:
likes = 1
```

But we can't just sum up likes from both servers because we don't know if those are likes from different users.

So to implement CRDT, we store additional information about from who are those likes:
```
Replica A:
A = 1
B = 0

Replica B:
A = 0
B = 1
```

where A, B represents different users. Now we can merge data from both replicas:
```
A = 1
B = 1
```
So total likes is 2.
# Properties
- Commutative - Order doesn't matter - `merge(A,B) = merge(B,A)`
- Associative - Grouping does not matter:` merge(A, merge(B,C)) = merge(merge(A,B),C)`
- Idempotent - Applying the same update twice does not change the result: `merge(A,A)=A`
# Types of CRDTs
## Counter CRDT
Good for:
- likes
- views
- downloads

Example:
```
likes += 1
```
## Set CRDT
Example: A user adds tags.

Replica A:
```
{red, blue}
```

Replica B:
```
{green, blue}
```

Merge:
```
{red, blue, green}
```
## Register CRDT
Stores a single value. Similar to LWW, but with formal conflict rules.