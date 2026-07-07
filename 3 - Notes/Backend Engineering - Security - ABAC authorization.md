Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
ABC is an authorization method where we decide whether an action is allowed or denied based on attributes / properties of:
- user
- resource
- environment

All those attributed must satisfy a specific conditions in order to get permission.
# Example attributes
## User attributes:
- department = “finance”
- role = “manager”
- location = “EU”
## Resource attributes:
- documentType = “financial”
- owner = “user123”
## Environment:
- time = “business hours”
- device = “company laptop”
# Example rules
> “Allow access if user is in finance department AND document is financial data”

or

> “Allow access only if user is accessing from company network”

# Benefits
- Very flexible
- Gives a precise control
- Scales better for complex systems (it works better when there is a lot of rules which determine permission)
# Drawbacks
- More complex to design
- Harder to debug
- Requires policy engine
# Questions
- What is a policy engine?