Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Two pointers** is an algorithmic technique where you use **two variables (pointers/indices) to traverse a data structure**, usually an array or string, to reduce unnecessary work.

Instead of using nested loops (`O(n²)`), two pointers often achieve `O(n)`.
# Example: find a pair with a target sum
Sorted array:
```
[1, 2, 4, 6, 8, 10]

Target = 10
```

Use two pointers:
```
left → 1  2  4  6  8  10 ← right
```

Steps:
- `1 + 10 = 11` → too large → move right left
- `1 + 8 = 9` → too small → move left right
- `2 + 8 = 10` → found

Complexity:
```
O(n)
```

instead of checking every pair:
```
O(n²)
```
# Common patterns
## 1. Opposite directions
Pointers start at both ends:
```
left → [ ... ] ← right
```

Used for:
- two-sum in sorted arrays
- reversing arrays
- palindrome checking
## 2. Same direction (slow/fast pointers)
Example:
```
slow →
fast →→
```

Used for:
- removing duplicates
- detecting cycles in linked lists
- finding middle of a linked list
# Why it works
The key idea is:
> Move pointers intelligently so each element is processed only a small number of times.
# Where used in software engineering
Two pointers are common in:
- searching algorithms
- string processing
- data processing pipelines
- memory-efficient algorithms

Mental model:
```
Brute force:
compare everything with everything → O(n²)

Two pointers:
move through data once → O(n)
```

It is one of the most common algorithmic patterns to recognize.