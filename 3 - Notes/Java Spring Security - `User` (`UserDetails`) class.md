Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
`UserDetails` is an interface representing the information Spring Security needs about an authenticated user.

`User` is an implementation of this interface:
```java
org.springframework.security.core.userdetails.User
```
# Use case - `UserDetailsService`
The `UserDetails` interface is used in the `UserDetailsService` interface ([[Java Spring Security - `UserDetailsService` - Loading user data|link]]). The `UserDetailsService.loadUserByUsername()` method returns an object that implements the `UserDetails` interface.
# Construct a user
We can construct a user like that:
```java
User.withUsername(user.getEmail())
    .password(user.getPasswordHash())
    .authorities("USER")
    .build();
```

Here:
- `withUsername()` starts constructing a user and sets the username.    
- `password()` sets the stored password hash.    
- `authorities()` sets the permissions associated with the user.    
- `build()` creates the final `User` object.
## A. `withUsername()`
```java
User.withUsername(user.getEmail())
```

This is a static method that creates a builder and initializes it with the username.

Conceptually:
```java
UserBuilder builder = User.withUsername("john@example.com");
```

The builder is an object used to construct a `User`.
## B. `password()`
```java
.password(user.getPasswordHash())
```

Sets the stored password hash. This should be the encoded password stored in your database, not the original plaintext password.

Spring Security will later use a `PasswordEncoder` to compare the submitted password against this hash.
## C. `authorities()`
Assigns authorities to the user. Authorities represent permissions granted to the authenticated user.

For example:
```java
.authorities("USER", "ADMIN", "TASK_READ")
```

There is an important distinction:
- Authority: a specific permission or granted capability.    
- Role: conventionally an authority prefixed with `ROLE_`.    

For example:
```java
.roles("USER")
```

is equivalent to:
```java
.authorities("ROLE_USER")
```

So if you use `.authorities("USER")`, the authority is literally `USER`, not `ROLE_USER`.

Spring Security does not require these strings to come from a predefined list. However, your authorization configuration must use matching authority names.

A distinction worth remembering:
- `GrantedAuthority` is the interface representing an authority.    
- `SimpleGrantedAuthority` is a common implementation.    
- `authorities()` accepts authority strings and converts them into granted authorities.    

You can later enforce them using:
```java
.hasAuthority("ADMIN")
```

Or use role-based authorization:
```java
.hasRole("ADMIN")
```

`hasRole("ADMIN")` normally checks for the authority `ROLE_ADMIN`. This prefix distinction is important.
## D. `build()`
```java
.build();
```

Creates the actual Spring Security `User` object using the values configured in the builder.

The final result implements `UserDetails`, which is why it can be returned from `loadUserByUsername()`.
# Methods
There are multiple methods we can use with this class:

| Method                      | Purpose                                                |
| --------------------------- | ------------------------------------------------------ |
| `getUsername()`             | Returns the user's username/identifier                 |
| `getPassword()`             | Returns the stored password hash                       |
| `getAuthorities()`          | Returns the user's granted authorities                 |
| `isAccountNonExpired()`     | Indicates whether the account is still valid           |
| `isAccountNonLocked()`      | Indicates whether the account is locked                |
| `isCredentialsNonExpired()` | Indicates whether credentials are still valid          |
| `isEnabled()`               | Indicates whether the account is enabled               |
# Example authentication flow using `User`
Example authentication flow using `User` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].