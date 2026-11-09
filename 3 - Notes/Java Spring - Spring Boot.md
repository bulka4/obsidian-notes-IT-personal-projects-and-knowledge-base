Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
Spring Boot is built on top of the Spring Framework ([[_Java_Spring|link]]) and makes it easier to configure, develop and run Spring applications.

Without Spring Boot, you would typically need to configure many things manually.

Spring Boot provides:
- Auto-configuration: Automatically configures components based on dependencies and application settings.
- Starter dependencies: Convenient dependency bundles, such as spring-boot-starter-web.
- Embedded servers: Includes Tomcat, so you don't need to deploy your application to an external server.
- Production features: Health checks, metrics and monitoring integrations through Spring Boot Actuator.

For example, you can start your entire REST API with:
```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```