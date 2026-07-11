Tags: [[_Databases]]
#Databases  

# Introduction
An LSM-tree (Log-Structured Merge Tree) is a data structure used for organizing data and indexes ([[Databases - Indexes|link]]) which allows for very fast writes.

The key idea:
> Instead of updating the index/data structure immediately on disk, collect writes first and merge them later.
# How it works
## 1. Write to memory first
New writes go into a structure like a sorted in-memory table:
```
Memory (MemTable)

50 → row A
80 → row B
100 → row C
```

Very fast.
## 2. Store changes in a log
A write-ahead log (WAL) records the operation before applying it:
```
INSERT user_id=100
```
If the system crashes, the data can be recovered.
## 3. Periodically flush to disk
When memory is full, we save data from an in-memory table into a SSTable (sorted string table) which contains sorted key-value pairs (a value can me an entire multi-column row).
## 4. Merge files later (compaction)
Over time, SSTables are merged together:
```
SSTable 1:
10,20,50

SSTable 2:
30,50,100

New SSTable:
10,20,30,50,100
```
# Benefits
- Very fast writes
# Drawbacks
- Slower reads
