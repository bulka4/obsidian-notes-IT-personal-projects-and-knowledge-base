Tags: [[_Databases]]
#Databases  

# Introduction
A hash index is an index ([[Databases - Indexes|link]]) structure that uses a hash function where:
- A hash function converts an input value into a new value
- Multiple different inputs for a hash function can produce the same output.
- Hash output is assigned to a specific location (a bucket) which contains:
	- Only this one hash value
	- Information about which rows contains input values for which the hash function produced this output

So for example:
```
Hash("Alice") → Bucket 5
Hash("Bob")   → Bucket 5

Bucket 5:
    Alice → row 100
    Bob   → row 200
```
# Use cases
This method is good for exact lookups, for example:
```sql
WHERE username = 'Alice'
```
# Problems
There is no ordering so it is not good for:
- Range queries - `WHERE age > 30`
- Ordering - `ORDER BY age`