Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
A hash table is a data structure that stores key-value pairs and provides very fast lookup, insertion, and deletion.

Example:
```
Key        Value
----------------
"user1" → "Marcin"
"user2" → "Anna"
"user3" → "John"
```
# Searching through a hash table
Instead of searching through all elements, a hash table computes a hash for a key and that gives an index (a position) at which that key will be stored:
```
key → hash → index -> store value at the position given by the index
```

Thanks to this, the lookup is very fast because when we look for a value, we just need to calculate a hash for it and that gives us the position at which that value is stored if it exists:
```
key → hash → index -> retrieve value from the position given by the index
```
# Collisions
Different keys can produce the same index:
```
"user1" → index 42
"user5" → index 42
```

This is a collision.

Common solutions:
## 1. Chaining
- Store multiple values at the same index:
```
index 42:
    → user1
    → user5
```
## 2. Open addressing
- Find another empty location in the array.
# Complexity
Average case:

|Operation|Complexity|
|---|---|
|Insert|O(1)|
|Lookup|O(1)|
|Delete|O(1)|

Worst case (many collisions):

|Operation|Complexity|
|---|---|
|Insert|O(n)|
|Lookup|O(n)|
# Hash table vs database index
They solve a similar problem:
```
Find value by key quickly
```

but at different levels:
- **Hash table**
    - in-memory
    - very fast
    - usually used inside programs
- **Database index**
    - stored on disk
    - optimized for persistence and queries
# Why important in backend engineering
Hash tables are everywhere:
- caches:
    ```
    URL → cached response
    ```
- databases:
    ```
    user_id → user record
    ```
- distributed systems:
    ```
    key → service/node (consistent hashing)
    ```
- compilers:
    ```
    variable name → memory location
    ```

A good mental model:
```
Array → fast by position
Linked list → fast insertion/removal
Hash table → fast lookup by key
Tree → ordered data and range queries
```