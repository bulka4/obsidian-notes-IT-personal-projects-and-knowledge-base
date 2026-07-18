Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
ACL (Access Control List) is a mechanism that defines who can access a resource and what actions they are allowed to perform.
# ACL list format
An ACL is usually a list of rules like:
```
User A:
    can read file X
    cannot modify file X

User B:
    can read and write file X
```

General structure:
```
Principal (who)
        +
Resource (what)
        +
Action/Permission (what can be done)
        +
Allow/Deny
```
# Example
```
User: Alice
Resource: database.orders
Permission: READ
Decision: ALLOW
```

Meaning:
> Alice is allowed to read the `orders` table.
# Common ACL permissions
- Read
- Write
- Execute
- Create
- Delete
- Modify permissions
