Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Authentication testing** checks whether a system correctly verifies **who a user or service is**.

The question:
> "Can only legitimate users/services prove their identity and access the system?"

It tests things like:
- login with valid credentials
- login with invalid credentials
- password policies
- session handling
- token expiration
- multi-factor authentication
- account lockout mechanisms

Examples:
```
Valid username + password
        ↓
Access granted ✅
```

```
Wrong password
        ↓
Access denied ❌
```

```
Expired JWT token
        ↓
Request rejected ❌
```

Common authentication tests:
- Can users log in securely?
- Are passwords stored safely?
- Do sessions expire correctly?
- Can tokens be reused after logout?
- Are brute-force attempts handled?