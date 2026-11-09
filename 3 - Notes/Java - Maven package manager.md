Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Maven is the build and dependency management tool for Java projects.

Maven is responsible for:
1. Downloading external libraries (dependencies).
2. Managing dependency versions.
3. Compiling Java source code.
4. Running tests.
5. Packaging the application into a JAR file.
6. Running Spring Boot through Maven plugins.

It uses the `pom.xml` configuration file where we define the project.
# `pom.xml` file
[[Java - Maven package manager - `pom.xml` file]]
# How Maven works in practice
Here are the commands you will probably use most often.

|Command|Purpose|
|---|---|
|`mvn clean`|Deletes previously generated build files.|
|`mvn compile`|Compiles application source code.|
|`mvn test`|Executes automated tests.|
|`mvn package`|Builds the application JAR.|
|`mvn clean package`|Cleans and builds the application.|
|`mvn spring-boot:run`|Starts the Spring Boot application.|
|`mvn dependency:tree`|Displays the dependency hierarchy.|
