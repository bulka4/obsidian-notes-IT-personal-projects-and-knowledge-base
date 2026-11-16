Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
This is a collection of documents related to Java.
1. [[Java - Classpath]]
2. [[Java - jars]]
	1. [[Java - Standalone shaded jar]]
3. [[Java - Heap size]]
4. [[Java - Maven package manager]]
	1. [[Java - Maven package manager - `pom.xml` file]]
5. [[Java - JVM]]
6. [[Java - JDK]]
7. [[Java, Kotlin and Scala - Relation]]
# Benefits and drawbacks
1. [[Java vs Python]]
2. [[Java benefits - Developing large applications]]
3. [[Java benefits - Mature enterprise frameworks]]
# How Java works
1. [[Java - Heap and stack memory]]
	1. [[Java - Removing a reference variable vs removing an object from a heap memory]]
	2. [[Java - Memory garbage collector]]
# Syntax and features
1. [[Java - Static typing]]
2. [[Java - Complier]]
3. [[Java - Ternary operator]]
4. [[Java - Switch case]]
5. [[Java - Scanner - Input and output streams - `System.in` & `System.out`]]
6. [[Java - Logical operators]]
7. [[Java - IDEs - Support for large codebases and refactoring]]
8. [[Java - Concurrency
9. [[Java - Exception handling]]
	1. [[Java - Exception classes]]
	2. [[Java - Checked and unchecked exceptions]]
		1. [[Java - How the compiler check exceptions]]
10. [[Java - Modifiers]]
	1. [[Java - Access modifiers - Benefits]]
	2. [[Java - Non-access modifiers]]
11. [[Java - Working with files]]
12. [[Java - Working with dates and time]]
13. [[Java - Lambda expressions]]
14. [[Java - GUI desktop applications]]
15. [[Java - Scheduling tasks]]
16. [[Java - Threading]]
# Classes
1. [[Java - The main class and method]]
2. [[Java - Creating objects of classes]]
3. [[Java - Methods]]
	1. [[Java - Generic methods]]
4. [[Java - Annotations]]
5. [[Java - Overloaded methods]]
6. [[Java - Class constructors]]
7. [[Java - Class inheritance (extending a class)]]
8. [[Java - The `Object` class]]
9. [[Java - Abstract class]]
10. [[Java - Interface]]
	1. [[Java - Functional interface]]
	2. [[Java - Marker interface]]
	3. [[Java - Sealed interfaces]]
11. [[Java - Getters and setters]]
12. [[Java - Anonymous classes]]
13. [[Java - Generic classes]]
14. [[Java - `equals()` and `hashCode()`]]
	1. [[Java - `equals()` - Comparing objects]]
	2. [[Java - `hashCode()` - Calculating a hash]]
15. [[Java - Nested classes]]
16. [[Java - Record class]]
17. [[Java - Optional class]]
# Variables
1. [[Java - Data types - Primitive and Reference variables]]
	1. [[Java - Wrapper classes]]
2. [[Java - enum]]
3. [[Java - Variable scopes]]
4. [[Java - Arrays]]
	1. [[Java - ArrayList]]
	2. [[Java - Searching an array]]
5. [[Java - Stream]]
6. [[Java - Casting variables]]
7. [[Java - HashMap]]
# Spring
[[_Java_Spring]]
# Questions
- how to create authenticated user's principal, store it in a security context and pass to a controller using `@AuthenticationPrincipal`?

For later:
- Java Spring transactions

About my app:
- How the `TaskRepository` object is created in my app? How Spring creates and manages dependency objects?
- How `@AuthenticationPrincipal AuthenticatedUser currentUser` works, in the `TaskController.java`? How Spring creates the `currentUser` argument?
- What is the `UserDetailsService` class?
# To learn more about
- The last 3 sections here - [[Java - HashMap]] 
- How to create our own method parameter annotation - [[Java - Methods]]

About Spring:
1. IoC (Inversion of Control)
2. Spring IoC Container and ApplicationContext
3. Spring Beans
4. Bean registration (@Component, @Service, @Repository, @Bean)
5. Dependency Injection (constructor, setter, field)
6. Component scanning
7. Bean lifecycle
8. Bean scopes (singleton, prototype, request, session)
9. Bean configuration and profiles