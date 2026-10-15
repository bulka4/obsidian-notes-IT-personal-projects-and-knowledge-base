Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
ABC is an authorization method where we store rules which describe whether an action is allowed or denied based on attributes / properties of:
- user - who wants to access the resource
- resource - that the user wants to access
- environment - e.g. the current time, user's device used
# Example
For example, we might have a rule which checks a user's department:
```
ALLOW READ IF user.department == "Finance"
```
# Example attributes
Example attributes that we can use in rules:
- User attributes:
	- department = “finance”
	- role = “manager”
	- location = “EU”
- Resource attributes:
	- documentType = “financial”
	- owner = “user123”
- Environment:
	- time = “business hours”
	- device = “company laptop”
# Benefits
- Very flexible
- Gives a precise control
- Scales better for complex systems (it works better when there is a lot of rules which determine permission)
# Drawbacks
- More complex to design
- Harder to debug
- Requires policy engine
# Comparison to ACL
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
