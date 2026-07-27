Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Declarative programming is a programming style where you describe what you want to achieve, rather than how to achieve it.

You define the desired result, and the system decides the steps.

On the other hand there is imperative programming in which we define  exactly which steps the process should follow.
# Example
For example, SQL is declarative as we only say for example to select some columns and join tables:
```sql
select * from
	table1
	
	left join table2 on ...
```

and we don't specify exactly how tables will be joined as how data will be selected. The SQL database will prepare its own execution process which is out of our control.

While Python is imperative as we define exactly each step to follow, for example:
```python
total = 0

for item in items:
    total += item.price

print(total)
```
# No precise boundary
Although there is no precise boundary, what is declarative and imperative programming. We can only say that in declarative programming there is more things happening out of our contorl.

For example, when using Python there are still some things happening out of our control, e.g. how data is read from a memory of how CPU cores are used, but still usually we say that it is imperative because we control a lot (although not everything).