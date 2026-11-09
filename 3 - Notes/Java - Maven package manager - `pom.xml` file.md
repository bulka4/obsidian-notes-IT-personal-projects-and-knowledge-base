Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
`pom.xml` is a configuration file used by Maven ([[Java - Maven package manager|link]]) where we define the project.

It contains:
# Project information
```xml
<modelVersion>4.0.0</modelVersion>

<groupId>com.example</groupId>
<artifactId>todo-backend</artifactId>
<version>0.0.1-SNAPSHOT</version>
```

These elements identify your project.

| Element        | Meaning                                                           |
| -------------- | ----------------------------------------------------------------- |
| `modelVersion` | Version of the Maven project descriptor format.                   |
| `groupId`      | Identifies the organization or group responsible for the project. |
| `artifactId`   | Name of the project.                                              |
| `version`      | Version of your application.                                      |

Together, `groupId`, `artifactId` and `version` identify an artifact, for example:
```
com.example:todo-backend:0.0.1-SNAPSHOT
```
# Parent project
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.5.6</version>
    <relativePath/>
</parent>
```

This is particularly important.

Maven supports inheritance between project configurations.

By declaring `spring-boot-starter-parent` as the parent, your project inherits a collection of predefined configurations from Spring Boot.

For example, the parent manages:
- Versions of many dependencies.
- Default Maven plugin configurations.
- Java compilation settings.
- Resource processing configurations.

One of the biggest benefits is that you don't need to specify the version of every Spring dependency yourself.

For example, instead of writing:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>...</version>
</dependency>
```

You can simply write:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Spring Boot manages the appropriate version.

`relativePath` tells Maven where to look for a local parent POM. An empty value disables the default relative lookup, so Maven resolves the parent from its repositories.
# Properties
```xml
<properties>
    <java.version>21</java.version>
    <jjwt.version>0.12.6</jjwt.version>
</properties>
```

Properties are variables that you can reuse throughout the POM file.

For example:
```xml
<java.version>21</java.version>
```

Specifies that the project uses Java 21.

And:
```xml
<jjwt.version>0.12.6</jjwt.version>
```

Defines the version of the JWT library used by the project.

You can reference these properties using:
```xml
${java.version}
${jjwt.version}
```

This is useful because if you want to change a dependency version, you only need to change it in one place.
# Dependencies
This is probably the most important section of the file.
```xml
<dependencies>
    ...
</dependencies>
```

Dependencies are external libraries that your application needs.

When Maven builds your application, it downloads these libraries from Maven repositories (usually Maven Central).
# Build plugins
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

Maven plugins extend Maven's functionality.

While dependencies provide functionality to your application, plugins provide functionality to the build process.