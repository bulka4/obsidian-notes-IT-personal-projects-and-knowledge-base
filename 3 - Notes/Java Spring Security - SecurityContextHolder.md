Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
`SecurityContextHolder` - Stores the authenticated user's identity for the current request. It makes it available to the rest of the application.

We can create an authenticated `Authentication` object (`authentication.isAuthenticated() = true`) like this, using the `UsernamePasswordAuthenticationToken` class ([[Java Spring Security - `UsernamePasswordAuthenticationToken` class|link]]):
```java
var authentication =
    new UsernamePasswordAuthenticationToken(
        new AuthenticatedUser(userId, email),
        null,
        AuthorityUtils.NO_AUTHORITIES
    );
```

and pass it to the Security Context:
```java
SecurityContextHolder.getContext()
    .setAuthentication(authentication);
```

`SecurityContextHolder` makes that authentication information available to Spring Security during the current request without having to validate the token again.

For example, Spring Security can now:
- Recognize the request as authenticated.
- Allow access to endpoints requiring authentication.
- Provide the current user data in:
	- an endpoint through `@AuthenticationPrincipal` ([[Java Spring Security - `@AuthenticationPrincipal`|link]]).
	- filters used in `SecurityFilterChain` ([[Java Spring Security - `SecurityFilterChain` - Filters|link]])
- Check the user's authorities when performing authorization.
# Example authentication flow using `SecurityContextHolder`
Example authentication flow using `SecurityContextHolder` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].