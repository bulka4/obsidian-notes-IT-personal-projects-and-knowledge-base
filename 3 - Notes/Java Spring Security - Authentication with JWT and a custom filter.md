Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
This document describes how to implement an authentication flow with with JWT and a custom filter.

The main components we use are:

| Component               | Responsibility                                          |
| ----------------------- | ------------------------------------------------------- |
| `SecurityFilterChain`   | Configures HTTP security rules and filters              |
| `AuthenticationManager` | Coordinates authentication                              |
| `UserDetailsService`    | Loads user information from a user store                |
| `UserDetails`           | Represents user information required by Spring Security |
| `PasswordEncoder`       | Hashes passwords and verifies password matches          |
| `SecurityContextHolder` | Stores the current request's authenticated identity     |
| Custom JWT filter       | Extracts and validates JWT tokens                       |

and the main objects that we work with:

|Type|Purpose|
|---|---|
|`AppUser`|Application's database entity|
|`UserDetails`|User representation used during username/password authentication|
|`AuthenticatedUser`|Application-specific identity extracted from the JWT|
|`Authentication`|Spring Security object representing the authentication state|
# Classes
Classes that we use through the entire flow:
## 1. `SecurityConfig`
[[Java Spring Security - Authentication with JWT and a custom filter - `SecurityConfig`]]

We prepare configuration for the authentication flow in the `SecurityConfig` class.
## 2. `JwtService`
[[Java Spring Security - Authentication with JWT and a custom filter - `JwtService`]]

We prepare the `JwtService` class for generating and parsing JWT tokens.
## 3. `UserRepository`
[[Java Spring Security - Authentication with JWT and a custom filter - `UserRepository`]]

We prepare the `UserRepository` class to work with user data in the database.
# Flow overview
When a client sends a request, then:
## 1. `SecurityFilterChain`
[[Java Spring Security - Authentication with JWT and a custom filter - `SecurityFilterChain`]]

`SecurityFilterChain` ([[Java Spring Security - Defining security rules (`SecurityFilterChain`)|link]]) is applied to determine how to handle every request.

For example:
- which HTTP requests require authentication
- what filters ([[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]]) to use. In this case, the Custom JWT filter `JwtAuthenticationFilter`
## 2. Custom JWT filter 
[[Java Spring Security - Authentication with JWT and a custom filter - JWT filter]]

Custom JWT filter  (the `JwtAuthenticationFilter` class) is applied as specified in the `SecurityFilterChain`.

It can process the request:
- extract the token from the request (also checks if it is missing)
- extract claims from the token using `jwtService.parseClaims` (it also checks whether the token has expired)
- create an `authentication` object representing an authenticated user using `UsernamePasswordAuthenticationToken` ([[Java Spring Security - `UsernamePasswordAuthenticationToken` class|link]])
- The created `authentication` object is stored in the Security Context using `SecurityContextHolder.getContext().setAuthentication`
	- This makes the principal of the `authentication` object (i.e. user's data) available to subsequent security filters and application code handling this request
- Continue executing the remaining filters specified in the `SecurityFilterChain`
## 3. Route
A proper route from the REST Controller ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) now will handle the request.

We have different logic for routes that require and don't require authentication (it was defined in the `SecurityFilterChain` which routes require):
### 3.1 Routes that require authentication
[[Java Spring Security - Authentication with JWT and a custom filter - Providing user data in a route using `@AuthenticationPrincipal`]].

For routes that require authentication, the `@AuthenticationPrincipal` annotation ([[Java Spring Security - `@AuthenticationPrincipal`|link]]) will provide to the route the principal of the created `authentication` object from the Security Context representing an authenticated user, providing this user's data.
### 3.2 Routes that don't require authentication (Registration & Login)
[[Java Spring Security - Authentication with JWT and a custom filter - Registration & login routes]].

During Registration & Login:
- Client sends email and password to `POST /api/auth/register`
- `SecurityFilterChain` and Custom JWT filter (the `JwtAuthenticationFilter` class) are applied just like in case of the authenticated request but:
	- the filter checks whether a token is provided (using `header != null && header.startsWith("Bearer ")`)
	- During registration and login, the token is not provided, so the filter doesn't do anything, just goes to the next filter using `filterChain.doFilter(request, response);`
- Registration or Login route is executed
	- They both use `userRepository` to work with user data in the database
	- it is an extension of the `JpaRepository` class
#### 3.2.1 Registration route
Registration route:
- Normalizes the email from the request
- Uses `userRepository` to find out whether there is already a user with the provided email
- Uses `userRepository` to save in the database data of the new user
	- password is encoded using `passwordEncoder`
- Returns a response containing user's email and a new token (generated using `jwtService.generateToken`)
#### 3.2.2 Login route
Login route:
- Normalizes the email from the request
- Uses the `AuthenticationManager` ([[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`|link]]) to authenticate the user using provided credentials. It uses:
	- the implementation of the `UserDetailsService` interface to find the user in the database
	- The `PasswordEncoder` (defined in the `SecurityConfig`) to compare provided password with the one from the database
- Uses `userRepository` to get user's data from the database
- Returns a response containing user's email and a new token (generated using `jwtService.generateToken`)
# Practical considerations when modifying this implementation
These are particularly useful when developing authentication for other applications.

|Requirement|What you need to modify|
|---|---|
|Use username instead of email|`UserDetailsService`, registration/login DTOs, repository queries|
|Add user roles|Store roles in the database, return them from `UserDetailsService`, enforce them in security rules|
|Add account locking|Implement account status in `UserDetails` and configure account validation|
|Add token expiration|Change JWT expiration configuration|
|Add refresh tokens|Implement a separate refresh-token mechanism|
|Add logout|Implement token invalidation or another revocation strategy|
|Add permissions to endpoints|Use `hasAuthority()`, `hasRole()` or method-level security|
|Change password hashing|Configure another `PasswordEncoder` implementation|
|Change JWT claims|Modify `JwtService` and the JWT authentication filter|
|Add another authentication mechanism|Configure an appropriate authentication provider or filter|
