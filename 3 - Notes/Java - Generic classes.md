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