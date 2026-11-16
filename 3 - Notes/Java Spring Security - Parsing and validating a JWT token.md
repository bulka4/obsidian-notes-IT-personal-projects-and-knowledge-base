Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
```java
public Claims parseClaims(String token) {
    return Jwts.parser()
        .verifyWith((SecretKey) signingKey)
        .build()
        .parseSignedClaims(token)
        .getPayload();
}
```

This method is responsible for parsing a JWT token, verifying its digital signature, checking whether it expired, and extracting its claims (payload, data).

This method:
1. Creates a JWT parser.    
2. Configures the expected verification key.    
3. Parses the signed token.    
4. Verifies its signature.    
5. Checks token validity, including expiration.    
6. Returns the token's claims.    

If validation fails, the parsing operation throws an exception.

The signing key must be protected and kept outside source control, typically in environment-specific secrets or a secrets manager.
# Methods
What each method do:
## 1. `Jwts.parser()`
Creates a JWT parser using the JJWT library.

The parser knows how to read and validate JWT tokens.
## 2. `.verifyWith((SecretKey) signingKey)`
Provides the secret key used to verify the JWT signature.

Remember that when generating your JWT, you sign it using a secret key.

When receiving the JWT, you use the same key to verify that its signature is valid.

This helps ensure that the token hasn't been modified and was signed by someone possessing the correct key.
## 3. `.build()`
Builds the configured JWT parser.
## 4. `.parseSignedClaims(token)`
Parses the supplied token and verifies its signature.

It also checks standard JWT validation requirements, including expiration.

If the token is malformed, has an invalid signature, or is expired, parsing fails with an exception.
## 5. `.getPayload()`
Returns the JWT payload as a `Claims` object.
# What are Claims?
Claims are pieces of information stored inside the JWT payload.

For example, your application might generate a JWT with this payload:

```json
{
  "sub": "user@example.com",
  "userId": 123,
  "iat": 1794500000,
  "exp": 1794503600
}
```

These represent:

|Claim|Meaning|
|---|---|
|`sub`|Subject (in your case, user's email)|
|`userId`|Custom claim containing the user's ID|
|`iat`|Issued-at timestamp|
|`exp`|Expiration timestamp|

You can access them using the returned `Claims` object:
```java
Claims claims = parseClaims(token);

String email = claims.getSubject();
Integer userId = claims.get("userId", Integer.class);
Date expiration = claims.getExpiration();
```

The actual type of `userId` depends on how you encode it; for a Java `Long`, you may need to retrieve it as `Long` or convert it appropriately.
# Example authentication flow with JWT token
Example authentication flow using JWT token is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].