Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Non-access modifiers modify the behavior or characteristics of a declaration rather than controlling its accessibility.

| Modifier       | Meaning                                                                                      | Commonly applies to             |
| -------------- | -------------------------------------------------------------------------------------------- | ------------------------------- |
| `static`       | Belongs to the class rather than an individual object                                        | Fields, methods, nested classes |
| `final`        | Prevents certain changes or extensions                                                       | Variables, methods, classes     |
| `abstract`     | Declares something incomplete that must be implemented by a subclass (or implementing class) | Classes, methods                |
| `synchronized` | Controls concurrent access using a monitor lock                                              | Methods, blocks                 |
| `volatile`     | Provides visibility guarantees for shared variables between threads                          | Fields                          |
| `transient`    | Excludes a field from default Java serialization                                             | Fields                          |
| `native`       | Method implementation is provided outside Java                                               | Methods                         |
# `static`
A static method / variable belongs to the class itself, rather than an individual object.
```java
public class Calculator {

    public static int add(int a, int b) {
        return a + b;
    }
}
```

You can call it without creating an object:
```java
int result = Calculator.add(2, 3);
```

Without `static`, you generally need an object:
```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;
    }
}

// Usage:
Calculator calculator = new Calculator();
int result = calculator.add(2, 3);
```
# `final`
- A final method / variable cannot be overridden
- A final class can't be extended
```java
public final void validate() {}
```
# `abstract`
An abstract method / class ([[Java - Abstract class|link]]) has no implementation. A subclass must implement it unless that subclass is also abstract.
```java
public abstract void calculate();
```
It can only be declared in an abstract class or interface.
# `synchronized`
Controls access to a method when multiple threads are involved. Only one thread at a time can execute a synchronized instance method on a particular object (or a synchronized static method on the class monitor).
```java
public synchronized void updateBalance() {}
```
# `native`
Indicates that the method is implemented outside Java, typically in native code such as C or C++.
```java
public native void performOperation();
```
# `strictfp`
Historically controlled floating-point calculations to ensure consistent results. Since Java 17, floating-point expressions are always evaluated strictly, so this modifier is effectively unnecessary.
# `volatile`
Used with variables shared between threads.

It ensures that reads and writes to a variable are visible across threads, rather than relying on potentially stale thread-local cached values.
```
class Worker {
    private volatile boolean running = true;

    public void stop() {
        running = false;
    }

    public void work() {
        while (running) {
            // Do work
        }
    }
}
```

Without `volatile`, another thread might not observe the updated value promptly.

Important: `volatile` does not make compound operations such as `count++` atomic.
# `transient`
Used with fields that should not be included in default Java object serialization.
```
class User implements Serializable {
    String username;

    transient String password;
}
```

When serializing the object using Java's default serialization mechanism, the `password` field is excluded.

This can be useful when you don't want certain fields included in serialized objects.

Note that this is not a general-purpose way of securing sensitive data.