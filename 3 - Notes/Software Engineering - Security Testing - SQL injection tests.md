Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**SQL injection testing** checks whether an application is vulnerable to **malicious SQL code being inserted through user input**.

The question:
> "Can an attacker manipulate database queries by providing specially crafted input?"
# Example vulnerability
Application code:
```sql
SELECT * FROM users WHERE username = 'input';
```

User enters:
```sql
' OR '1'='1
```

The query becomes:
```sql
SELECT * FROM users WHERE username = '' OR '1'='1';
```

The condition is always true, potentially exposing data.
# SQL injection tests inputs
SQL injection tests try inputs like:
- quotes (`'`)
- SQL keywords
- unexpected operators
- specially crafted strings

They check whether:
- input is properly sanitized/escaped
- parameterized queries are used
- errors do not reveal database details
- unauthorized data cannot be accessed

Safe approach:
```sql
SELECT * FROM users WHERE username = ?
```

with the value passed separately (parameterized query).

SQL injection testing is a part of **security testing**, specifically under **input validation and database security testing**.