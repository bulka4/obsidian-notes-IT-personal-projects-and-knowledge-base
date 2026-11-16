Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
`AuthenticationManager` is the main Spring Security interface responsible for processing authentication requests.

Its primary method:
```java
Authentication authenticate(Authentication authentication);
```
receives authentication information and attempts to authenticate the user.

In this method
- Argument (`Authentication authentication`): Represents the authentication request submitted to the `AuthenticationManager`. Typically, `isAuthenticated()` is `false`.
- Return value (`Authentication`): Represents the result of authentication. If successful, `isAuthenticated()` is `true`, and it contains the authenticated principal and granted authorities.
# How it works
To learn more about how it works, checks this document - [[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`]].
# Example authentication flow using `AuthenticationManager`
Example authentication flow using `AuthenticationManager` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].
# Related topics
1. [[Java Spring Security - Creating the `authenticationManager`]]
2. [[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`]]