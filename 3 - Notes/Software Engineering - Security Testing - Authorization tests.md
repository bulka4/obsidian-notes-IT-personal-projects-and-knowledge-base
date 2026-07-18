Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Authorization testing** checks whether a user or service can access **only the resources and actions they are permitted to use**.

The question:
> "Even if someone is authenticated, are they allowed to do this?"
# Examples
## Role-based access
```
Admin:
  delete_user() ✅

Regular user:
  delete_user() ❌
```
## Resource access
```
User A:
  GET /users/A/profile ✅

User A:
  GET /users/B/profile ❌
```
## API permission testing
Check that:
- users cannot access other users' data
- regular users cannot perform admin actions
- services have only required permissions
- hidden endpoints cannot be accessed

Common authorization issues:
- **Privilege escalation** — gaining higher permissions than allowed
- **IDOR (Insecure Direct Object Reference)** — accessing another user's objects by changing an ID
- **Missing access checks** — endpoint works without verifying permissions

Difference:
- **Authentication:** "Who are you?"
- **Authorization:** "What are you allowed to do?"

Example:
```
User logs in successfully
        ↓
Authentication ✅

User tries to delete another user's account
        ↓
Authorization check ❌
```

Authorization testing is especially important for backend APIs, microservices, databases, and systems with role-based access control.