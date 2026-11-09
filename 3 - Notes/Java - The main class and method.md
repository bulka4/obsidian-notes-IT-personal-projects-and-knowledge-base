Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
To build a Java application, we need the `Main` class and `main` method:
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```
- `Main` is just a class name convention. We can name it anything.
- `main()` is the method the JVM uses as the starting point.
- `String[] args` contains command-line arguments.