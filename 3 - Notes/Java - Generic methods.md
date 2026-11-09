Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Generic methods allow us to work with different variable types. We provide a variable type as an argument:
```java
public static <T> void print(T value) {
    System.out.println(value);
}
```

Usage:

```java
print("Hello");
print(123);
print(3.14);
```

The compiler determines the type based on the argument.

Notice the `<T>` before the return type `void`. It declares the method's type parameter.
# Bounded generics
You can restrict which types are allowed.

For example:
```java
public static <T extends Number> void print(T value) {
    System.out.println(value);
}
```
- `<T extends Number>` declares a type parameter restricted to `Number` and its subclasses.
- `T` is the parameter's type.

Usage:
```java
print(10);    // Integer
print(3.14);  // Double
// print("Hi"); // Compile-time error
```

For multiple bounds:
```java
public static <T extends Number & Comparable<T>> void process(T value) {}
```

`T` must extend `Number` and implement `Comparable<T>`.