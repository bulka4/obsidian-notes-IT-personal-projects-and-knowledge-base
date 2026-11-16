Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Generic classes allow us to work with different variable types. We provide a variable type as an argument:
```java
public class Box<T> {

    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

Here, `T` is a type parameter. It represents a type that will be specified later.

You can create objects using different types:
```java
Box<String> stringBox = new Box<>();
stringBox.setValue("Hello");

Box<Integer> integerBox = new Box<>();
integerBox.setValue(123);
```

The same `Box` class works with different types.

`T` is just a conventional name. You can use other names too.
# Bounded generics
You can restrict which types are allowed.

For example:
```java
public class Calculator<T extends Number> {

    private T value;

    public Calculator(T value) {
        this.value = value;
    }
}
```
- `<T extends Number>` declares a type parameter restricted to `Number` and its subclasses.
- `T` is the parameter's type.

Now you can use:
```java
Calculator<Integer> c1 = new Calculator<>(10);
Calculator<Double> c2 = new Calculator<>(10.5);
```

But you cannot use:
```java
Calculator<String> c3 = new Calculator<>("Hello"); // Error
```

Because `String` does not extend `Number`.

For multiple bounds:
```java
public class Calculator <T extends Number & Comparable<T>> {}
```

`T` must extend `Number` and implement `Comparable<T>`.
# Extending a generic class
When we create a child class that extends a parent class ([[Java - Class inheritance (extending a class)|link]]), there are a few common options for how we can do that:
## 1. Child preserves the parent's generic parameters
```java
class Parent<T> {
    T value;
}

class Child<T> extends Parent<T> {
}
```

Here, `Child` is also generic. It passes its own type parameter `T` to the parent.

You can then write:
```java
Child<String> child = new Child<>();
```
## 2. Child specifies a concrete type
```java
class Parent<T> {
    T value;
}

class Child extends Parent<String> {
}
```

Here, `Child` is not generic. It always inherits `Parent` with `T = String`.

You can write:
```java
Child child = new Child();
```

But not `Child<Integer>`.