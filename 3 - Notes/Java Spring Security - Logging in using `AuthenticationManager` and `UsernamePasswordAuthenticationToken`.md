Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
We can use `UsernamePasswordAuthenticationToken` class ([[Java Spring Security - `UsernamePasswordAuthenticationToken` class|link]]) to create an object (unauthenticated object of the `Authentication` class) which represents authentication request containing credentials:
```java
// Create an unauthenticated Authentication object
Authentication authentication = new UsernamePasswordAuthenticationToken(
    email,
    request.password()
);
```

and pass it to an object of the `AuthenticationManager` interface ([[Java Spring Security - `AuthenticationManager` interface|link]]) so that Spring Security attempts to authenticate the user using supplied email and password:
```java
Authentication authentication =
    authenticationManager.authenticate(
        new UsernamePasswordAuthenticationToken(
            email,
            request.password()
        )
    );
```

If authentication succeeds, then the `Authentication authentication` object represents an authenticated user.
# How it works
Conceptually, the process is:
1. `AuthenticationManager` receives the authentication request.
2. An appropriate authentication provider (`AuthenticationProvider`) processes it.
	1. It is used internally inside `authenticationManager.authenticate`
3. The provider calls `UserDetailsService.loadUserByUsername()` ([[Java Spring Security - `UserDetailsService` - Loading user data|link]])
4. It retrieves the user's password hash.
5. It uses `PasswordEncoder.matches()` to verify the password.
	1. `PasswordEncoder` needs to be registered as a bean (defined in the `@Configuration` ([[Java Spring Security - Security configuration|link]]))
6. If valid, it returns an authenticated `Authentication` object.
7. If invalid, authentication fails, normally with an `AuthenticationException`.

Important: `AuthenticationManager` is an abstraction. It does not necessarily perform all these operations itself. An `AuthenticationProvider` handles the actual authentication mechanism.
# Requirements
We need to prepare:
- Implementation of the `UserDetailsService.loadUserByUsername()` ([[Java Spring Security - `UserDetailsService` - Loading user data|link]])
- Implementation of the `PasswordEncoder` ([[Java Spring Security - `PasswordEncoder`|link]])

They need to be both registered as beans ([[Java Spring - Bean|link]]).
# Example authentication flow using `AuthenticationManager`
Example authentication flow using `AuthenticationManager` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].