Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
```java
public String generateToken(Long userId, String email) {
    Date now = new Date();

    return Jwts.builder()
        .subject(email)
        .claim("userId", userId)
        .issuedAt(now)
        .expiration(new Date(now.getTime() + expirationMs))
        .signWith(signingKey)
        .compact();
}
```

Important methods:

|Method|Purpose|
|---|---|
|`subject()`|Sets the token subject, here the user's email|
|`claim()`|Adds a custom claim|
|`issuedAt()`|Sets token creation time|
|`expiration()`|Sets token expiration|
|`signWith()`|Signs the token using a cryptographic key|
|`compact()`|Produces the final JWT string|

A claim is simply a piece of information stored in the JWT payload.

Your example includes:
- Subject: email.    
- Custom claim: user ID.    
- Issued-at timestamp.    
- Expiration timestamp.
# Example authentication flow with JWT token
Example authentication flow using JWT token is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].