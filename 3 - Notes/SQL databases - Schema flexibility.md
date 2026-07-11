Tags: [[_Databases]]
#Databases  

# Introduction
In SQL databases, schema changes (e.g. adding a new column) can be problematic, much more than in case of NoSQL databases ([[NoSQL databases - Schema flexibility|link]]).

When adding a new column:
- It affects the entire table (all the existing records)
- If that column can't contain null values, then all the existing records need to have inserted a new value in this column.
- It will have an impact on the result of `select * from` used in all the systems that uses this database (which can cause problems)