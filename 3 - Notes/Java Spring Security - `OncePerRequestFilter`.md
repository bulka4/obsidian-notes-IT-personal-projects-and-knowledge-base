Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
It is a Spring Web filter base class.

It provides a mechanism for executing filter logic once per request within a single request thread.

You extend it when you want to implement custom HTTP request processing.

It is commonly used for:
- JWT authentication.    
- Request logging.    
- Custom request validation.    
- Security-related request processing.
# Example authentication flow using `OncePerRequestFilter`
Example authentication flow using `OncePerRequestFilter` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].