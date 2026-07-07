Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
An **API key** is a simple string used to identify and authenticate an application (not a user) when it calls an API.
# What it is used for
API keys mainly answer:
> “Which application is making this request?”

They are commonly used for:
- tracking usage
- rate limiting
- basic access control
- billing (who used how much API)
# How it works
1. Developer registers an app with a service (e.g., Google Maps)
2. Service issues an API key
3. App sends key with every request
```
GET /maps?location=paris
x-api-key: ABC123
```
4. Server checks:
	- is key valid?
	- is it active?
	- what quota is left?
# What API keys are NOT
API keys are not strong user authentication:
- they usually do NOT identify individual users
- they do NOT replace login systems
- they are often not secret enough alone for sensitive actions
