Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
ACL (Access Control List) is an authorization mechanism which stores in a list rules about which actions all the users are allowed to perform on which resources.

Each element of that list consists of fields:
- user
- resource
- permission
- decision

and specifies whether or not a specific action is allowed for a specific user and a resource.
# Example
For example, an ACL list can contain an element with attributes:
```
User: Alice
Resource: database.orders
Permission: READ
Decision: ALLOW
```

which means that the Alice user can read from the `database.orders` table.
# Common ACL permissions
- Read
- Write
- Execute
- Create
- Delete
- Modify permissions
# Comparison to ABAC
In ABAC, stored rules are based on attributes of a user and a resource while in ACL stored rules refer to a specific user and resource.

For example, in ABAC we might store a rule like this:
```
ALLOW READ IF user.department == "Finance"
```

which might refer to many users (all from a specific department), while a rule in ACL will be always for a specific user:
```
User: Alice
Resource: database.orders
Permission: READ
Decision: ALLOW
```
