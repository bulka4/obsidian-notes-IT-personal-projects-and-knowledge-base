Tags: [[_Databases]]
#Databases  

# Introduction
Data integrity constraints are rules describing what values are allowed in a database. Those rules might be for example:
# Domain constraints (allowed values)
Rules specifying what values are allowed, for example:
- Bigger than 0
- Must be one of allowed values (e.g. 'pending', 'approved', 'rejected')
# Entity integrity (row identity)
Rules about identifying rows, for example:
- Value can't be empty
- Values must be unique
# Referential integrity (relationships)
Rules about relationships between tables, for example:
- Value must exist in a column in another table
# Business rules
More complex rules, for example:
- `start_date` < `end_date`
- Sum of some values must be always the same