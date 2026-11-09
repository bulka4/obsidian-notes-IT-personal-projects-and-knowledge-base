Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A functional interface is an interface that has exactly one abstract method.

For example:
```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}
```

The `@FunctionalInterface` annotation tells the compiler that this interface is intended to be functional. The compiler will report an error if you add another abstract method.

You can implement it using a regular class:
```java
class Addition implements Calculator {
    @Override
    public int calculate(int a, int b) {
        return a + b;
    }
}
```

or using an anonymous class ([[Java - Anonymous classes|link]]):
```java
Calculator calculator = new Calculator() {
    @Override
    public int calculate(int a, int b) {
        return a + b;
    }
};
```

Or using a lambda:
```java
Calculator addition = (a, b) -> a + b;

int result = addition.calculate(5, 10);
```

When using lambda, Java knows that:
- The interface has one abstract method.
- That method accepts two integers.
- That method returns an integer.

Therefore, it can determine what the lambda expression represents. We don't need to explicitly specify parameter types:
```java
Calculator calculator = (int a, int b) -> a + b;
```

**Important**: A functional interface can have additional methods, provided they are not additional abstract methods.
# Built-in functional interfaces
Java provides several commonly used functional interfaces in the `java.util.function` package.

You don't need to define your own functional interface every time.

The most important ones are:
## Predicate
Accepts an argument and returns a boolean.
```java
Predicate<Integer> isAdult = age -> age >= 18;

System.out.println(isAdult.test(25)); // true
```

Useful for checking conditions and filtering data.
## Function
Accepts an argument and returns a result.
```java
Function<String, Integer> getLength = text -> text.length();

int length = getLength.apply("Hello"); // 5
```

Useful for transforming data.
## Consumer
Accepts an argument but doesn't return anything.
```java
Consumer<String> printer = text -> System.out.println(text);

printer.accept("Hello!");
```

Useful for performing actions on objects.
## Supplier
Doesn't accept arguments but returns a result.
```java
Supplier<Double> randomNumber = () -> Math.random();

double number = randomNumber.get();
```

Useful for generating or providing values.