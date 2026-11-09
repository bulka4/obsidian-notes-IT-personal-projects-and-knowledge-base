Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A sealed interface restricts which classes or interfaces can implement or extend it.

For example:
```java
sealed interface Shape
    permits Circle, Rectangle {
}

final class Circle implements Shape {
}

final class Rectangle implements Shape {
}
```

Only `Circle` and `Rectangle` are permitted to implement `Shape` directly.

This is useful when you want to control the possible implementations of an interface.

For example, you might have a payment system supporting only a predefined set of payment types.

Sealed interfaces were introduced in Java 17.