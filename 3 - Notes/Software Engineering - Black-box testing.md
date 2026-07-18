Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Black-box testing is a testing approach where you test a system without knowing or depending on its internal implementation.

We only care about:
- inputs
- outputs
- observable behavior

The system is treated like a "black box".
# Example: Testing a login API
We do not care how authentication is implemented, we only verify the behavior:
```
POST /login

Input:
{
  "username": "alice",
  "password": "123"
}

Expected output:
200 OK + token
```
# What black-box tests check
- Does the system produce correct outputs?
- Does it handle invalid inputs?
- Does it satisfy requirements?
- Does it behave correctly from a user's perspective?