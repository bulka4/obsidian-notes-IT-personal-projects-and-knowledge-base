Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
The `UsernamePasswordAuthenticationToken` class is an implementation of the `Authentication` interface ([[Java Spring Security - `Authentication` interface|link]]).
# The `authenticated` attribute
The `UsernamePasswordAuthenticationToken` class contains:
- the `authenticated` boolean attribute 
- the `IsAuthenticated()` method
indicating whether or not a user is authenticated
# Constructor arguments
Arguments of the constructor for this class are:
```java
UsernamePasswordAuthenticationToken(
	principal,
	credentials,
	authorities
)
```
- principal - user identity
- credentials - authentication credentials
- authorities - granted permissions/roles
# How to use it
We can use it for:
- Creating an authentication request which is passed to `authenticationManager` to authenticate the user (login) - [[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`|link]] 
- Representing an authenticated user and use it in a JWT filter - [[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]] 
## A. Creating an authentication request
We can use `UsernamePasswordAuthenticationToken` class to create an object (unauthenticated object of the `Authentication` interface) which represents authentication request containing credentials:
```java
// Create an unauthenticated Authentication object
Authentication authentication = new UsernamePasswordAuthenticationToken(
    email,
    request.password()
);
```

It can be then passed to an object of the `AuthenticationManager` interface ([[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`|link]]) so that Spring Security attempts to authenticate the user using supplied email and password.
## B. Representing an authenticated user
The `UsernamePasswordAuthenticationToken` class can also create an authenticated `Authentication` object (`authentication.isAuthenticated() = true`) like this:
```java
var authentication =
    new UsernamePasswordAuthenticationToken(
        new AuthenticatedUser(userId, email),
        null,
        AuthorityUtils.NO_AUTHORITIES
    );
```

this `authentication` object represents an authenticated user (given by `AuthenticatedUser(userId, email)`).

It can be then stored in the security context ([[Java Spring Security - SecurityContextHolder|link]]):
```java
SecurityContextHolder.getContext()
    .setAuthentication(authentication);
```

This makes that authentication information available to Spring Security during the current request.

We can create one in a JWT filter ([[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]]).
# Example authentication flow using the `UsernamePasswordAuthenticationToken` class
Example authentication flow using the `UsernamePasswordAuthenticationToken` class is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].