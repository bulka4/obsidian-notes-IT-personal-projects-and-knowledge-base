Tags: [[__My_projects]]
#MyProjects 

# Java libraries
Tools used:
- Java 21
- Spring Boot - Framework for building applications. Provides the underlying functionality for dependency injection, web applications, transactions, and much more.
- Hibernate - JPA implementation that handles object-relational mapping
- BCrypt - Hashing user passwords
- Maven - manages dependencies and builds the Java application.

Java libraries used, defined in the `pom.xml` file:
- Spring Web - Provides functionality for building HTTP applications and REST APIs
	- Includes Spring MVC and an embedded Tomcat server.
- Spring Data JPA - Provides functionality for interacting with relational databases
- Spring Security - Provides authentication and authorization functionality
- Spring Validation - Provides validation functionality for incoming data
- JJWT library modules for generating JWT tokens
- H2 relational database, used for development so we don't need to deploy separate SQL databases
- Spring Boot Test - Provides libraries for automated testing
- Spring Boot Maven plugin - provides Spring Boot-specific build functionality
# Database
We use H2 relational database, used for development so we don't need to deploy separate SQL databases.

It is installed using Maven, defined in the `pom.xml` file.