Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
`PasswordEncoder` hashes passwords and verifies password matches. Passwords should not be stored directly in the database.

We define it in the Security Config ([[Java Spring Security - Security configuration|link]]).

`BCryptPasswordEncoder` implements Spring Security's `PasswordEncoder` interface.

The interface provides two particularly important methods:
```java
String encode(CharSequence rawPassword);

boolean matches(
    CharSequence rawPassword,
    String encodedPassword
);
```
- `encode()` hashes a plain-text password.    
- `matches()` checks whether a plain-text password corresponds to an existing hash.    
# Registration
```java
passwordEncoder.encode(request.password())
```

The application hashes the password before saving the user.
# Login
We can use `AuthenticationManager` ([[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`|link]]) to perform login and it will use automatically the `passwordEncoder` method defined in the Security Config ([[Java Spring Security - Security configuration|link]]). We don't need to use it on our own.

Important: BCrypt uses a random salt. Consequently, encoding the same password twice can produce different hashes. This is why you must use `matches()` rather than comparing hashes directly.
# Where to define it
We can define it and register as a bean in a security configuration - [[Java Spring Security - Security configuration|link]].
# Example authentication flow using `PasswordEncoder`
Example authentication flow using `PasswordEncoder` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].