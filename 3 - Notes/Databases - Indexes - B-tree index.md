Tags: [[_Databases]]
#Databases  

# Introduction
A B-tree index ([[Databases - Indexes|link]]) is a balanced tree structure that keeps indexed values sorted and allows the database to find data without scanning the whole table.
# How it works
## Creating a tree
We start with all the values from a table as a single node:
```
10, 20, 30, 40, 50
```

If there is too many values in a single node, then we split it by moving the middle key up to the parent. So in this case, we create a tree like that:
```
		[10]
	  /      \
  [10, 20]  [40, 50]
```

We continue doing this for all nodes until no node has more elements than established limit.
## Searching for a value
When we search for a specific value, for example `WHERE id = 20`, we start at the root and compare values:
```
20 > 10
```
then we go left or right depending on whether our value is bigger or smaller than the root value. In this case, we go left:
```
[20,30]
```
and we find our value 20. 

Together with this value, there is stored information about which row contains this value:
```
20 → row location
```
this way, we find a specific row with the value we are looking for.
# Properties
- balanced tree
- sorted data
- fast search
- It has a complexity `O(log n)`
# Use cases
It is good for:
- Equality - `WHERE id = 100`
- Range queries - `WHERE id BETWEEN 0 and 100`
- Sorting - `ORDER BY age`
