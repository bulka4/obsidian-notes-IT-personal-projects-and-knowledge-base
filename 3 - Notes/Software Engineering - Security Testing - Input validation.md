Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Input validation testing checks whether a system properly handles and rejects invalid, unexpected, or malicious input.

The question:
> "Does the system safely handle everything users or external systems send to it?"
# Examples
## Invalid data
```
Age field:

Input:
"abc"

Expected:
Rejected ❌
```
## Too large input
```
Username:
10 million characters

Expected:
Rejected safely
```
## Malicious input
```
SQL:
' OR 1=1 --

Expected:
Blocked / treated as normal text
```

It tests:
- correct data types
- allowed ranges
- required fields
- input length limits
- special characters
- file uploads
- API request validation

It helps prevent:
- SQL injection
- command injection
- buffer overflows
- malformed data entering the system
- crashes caused by unexpected input

Example:
```
API receives request
        ↓
Validate input
        ↓
Valid → process request
Invalid → reject safely
```