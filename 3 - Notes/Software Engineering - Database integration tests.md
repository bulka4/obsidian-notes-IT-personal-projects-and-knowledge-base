Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Database integration tests verify that our application works correctly together with a real database (or a realistic database environment):
- They test the interaction between our code and the database, not just individual functions.
- Unit tests can be done on a fake database (i.e. use in-memory objects, e.g. Python lists / dataframes instead of a real database) while integration ones use a real one.
# What they check
## SQL correctness
Catches:
- wrong SQL
- wrong table names
- wrong joins
- wrong column mappings
## Database schema compatibility
Verifies the application still works with the new schema (e.g. different column names, new column).
## Transactions
Test:
- rollback works
- failures do not leave inconsistent data
## Constraints
Set up some rule, e.g. `email UNIQUE`, try to violate that rule and check whether we get an error, for example:
```
Insert:
alice@example.com

Insert again:
alice@example.com

Expected:
Constraint violation
```
# Typical setup
Usually, we set up a test database that may run using for example:
- Docker container
- temporary database
- test schema

We don't use a production one since tests should be:
- isolated
- repeatable
- safe

and we don't want to modify the production database.