Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
JWT (JSON Web Token) is format of an access token used in a token-based authentication ([[Backend Engineering - Security - Token-based authentication|link]]).
# What a JWT looks like
A JWT is a string with 3 parts:
```
header.payload.signature
```

`header` - Describes the token type and algorithm
  ```
	{
	  "alg": "HS256",
	  "typ": "JWT"
	}
  ```

`payload` - Contains user data
  ```
	{
	  "userId": 123,
	  "role": "admin",
	  "exp": 1710000000
	}
  ```

`signature` - Created using a secret key:
  ```
	HMACSHA256(header + payload, secret)
  ```
# Important features
## Not encrypted by default
Payload is readable by anyone, so never put secrets (passwords, sensitive data) inside JWT.