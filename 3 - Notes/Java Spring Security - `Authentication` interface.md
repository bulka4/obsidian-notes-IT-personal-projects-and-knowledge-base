Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
`Authentication` is an interface in Spring Security that represents an authentication request or an authenticated user.

It is one of the central concepts in Spring Security because it carries information about:
- Who is trying to authenticate or who has been authenticated.    
- What credentials were provided.    
- What authorities the user has.    
- Whether authentication has succeeded.    

Think of it as an object representing the current authentication state of a user.
# Attributes
- principal - user identity
- credentials - authentication credentials
- authorities - granted permissions/roles
# Methods
The interface provides several important methods:

| Method              | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| `getPrincipal()`    | Returns the identity of the user.                           |
| `getCredentials()`  | Returns the credentials, usually a password during login.   |
| `getAuthorities()`  | Returns the user's granted authorities.                     |
| `getName()`         | Returns the user's identifier, typically username or email. |
| `isAuthenticated()` | Indicates whether authentication has succeeded.             |

For example, after successful authentication, an `Authentication` object might conceptually contain:
```java
Authentication authentication = ...;

authentication.getName();        // "user@example.com"
authentication.getPrincipal();   // UserDetails object
authentication.getCredentials();// Usually empty/null after authentication
authentication.getAuthorities();// [ROLE_USER]
authentication.isAuthenticated();// true
```
# Implementations of the Authentication interface
Spring Security provides different implementations of `Authentication`.

One particularly important implementation is `UsernamePasswordAuthenticationToken` ([[Java Spring Security - `UsernamePasswordAuthenticationToken` class|link]]).
# Example authentication flow using the `Authentication` interface
Example authentication flow using the `Authentication` interface is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].