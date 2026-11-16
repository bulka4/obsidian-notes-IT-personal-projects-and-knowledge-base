Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
The `JwtService` class contains methods for generating ([[Java Spring Security - Generating a JWT token|link]]) and parsing ([[Java Spring Security - Parsing and validating a JWT token|link]]) JWT tokens:
```java
@Service
public class JwtService {
    private final Key signingKey;
    private final long expirationMs;

    public JwtService(
        @Value("${app.jwt.secret}") String secret,
        @Value("${app.jwt.expiration-ms}") long expirationMs
    ) {
        this.signingKey = Keys.hmacShaKeyFor(Decoders.BASE64.decode(secret));
        this.expirationMs = expirationMs;
    }

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

    public Claims parseClaims(String token) {
        return Jwts.parser()
            .verifyWith((javax.crypto.SecretKey) signingKey)
            .build()
            .parseSignedClaims(token)
            .getPayload();
    }
}
```
# `parseClaims`
The `parseClaims` method ([[Java Spring Security - Parsing and validating a JWT token|link]]) is responsible for parsing a JWT token, verifying its digital signature, checking whether it expired, and extracting its claims (payload, data).

This method:
1. Creates a JWT parser.    
2. Configures the expected verification key.    
3. Parses the signed token.    
4. Verifies its signature.    
5. Checks token validity, including expiration.    
6. Returns the token's claims.    

If validation fails, the parsing operation throws an exception.

The signing key must be protected and kept outside source control, typically in environment-specific secrets or a secrets manager.
# `generateToken`
The `generateToken` method ([[Java Spring Security - Generating a JWT token|link]]) is used to generate the token.