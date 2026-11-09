Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
In Java, an anonymous class is a class that you define and instantiate at the same time, without giving it a name. This class needs to be either an extension of another class ([[Java - Class inheritance (extending a class)|link]]) or an implementation of an interface ([[Java - Interface|link]]).
# Example
## Implementing an interface
For example:
```java
interface Greeting {
    void sayHello();
}

Greeting greeting = new Greeting() {
    @Override
    public void sayHello() {
        System.out.println("Hello!");
    }
};

greeting.sayHello();
```

Instead of defining a separate class that implements this interface:
```java
interface Greeting {
    void sayHello();
}

class EnglishGreeting implements Greeting {
    @Override
    public void sayHello() {
        System.out.println("Hello!");
    }
}

Greeting greeting = new EnglishGreeting();

greeting.sayHello();
```
## Extending a class
```java
class Animal {
    public void makeSound() {
        System.out.println("Some sound");
    }
}

Animal animal = new Animal() {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
};

animal.makeSound();
```
# Anonymous classes can access local variables
An interesting feature is that anonymous classes can access variables from the surrounding scope.

For example:
```java
String message = "Hello from outside!";

Greeting greeting = new Greeting() {
    @Override
    public void sayHello() {
        System.out.println(message);
    }
};
```

However, there is an important restriction: local variables accessed by an anonymous class must be `final` or effectively final ([[Java - Non-access modifiers|link]]).

Effectively final means that you don't explicitly declare a variable as `final`, but you also don't reassign it after initialization.

This is allowed:
```java
String message = "Hello";

Greeting greeting = new Greeting() {
    @Override
    public void sayHello() {
        System.out.println(message);
    }
};
```

This is not allowed:
```java
String message = "Hello";

Greeting greeting = new Greeting() {
    @Override
    public void sayHello() {
        System.out.println(message);
    }
};

message = "Goodbye"; // Compilation error
```

The reason is related to how Java captures local variables for use inside inner classes.
# Anonymous classes and lambda expressions
This is particularly important because anonymous classes are closely related to lambda expressions.

Consider this interface:
```java
interface Calculator {
    int calculate(int a, int b);
}
```

You can implement it using an anonymous class:
```java
Calculator calculator = new Calculator() {
    @Override
    public int calculate(int a, int b) {
        return a + b;
    }
};
```

However, Java also supports lambda expressions:
```java
Calculator calculator = (a, b) -> a + b;
```

Both create an implementation of the `Calculator` interface.

Why can we use a lambda here?

Because `Calculator` is a functional interface: an interface with exactly one abstract method.

Lambdas provide a shorter syntax for implementing functional interfaces.

Here's a comparison:

|Anonymous class|Lambda|
|---|---|
|Can implement interfaces|Can implement functional interfaces|
|Can extend classes|Cannot extend classes|
|Can implement multiple methods|Implements one abstract method|
|Has its own `this` reference|`this` refers to the surrounding object|
|More verbose|More concise|

For example, consider Java's `Runnable` interface:
```java
Runnable task = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running task...");
    }
};
```

The lambda equivalent:
```java
Runnable task = () -> System.out.println("Running task...");
```

Both can be executed with:
```java
task.run();
```
# When are anonymous classes useful?
Some common use cases:

1. Event listeners

For example, when handling a button click in a Java GUI application:
```java
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button clicked!");
    }
});
```

2. Customizing behavior

When you need to override a method for one particular object without creating a separate class.

3. Implementing interfaces temporarily

When you need a quick implementation of an interface without creating a separate class.

4. Working with APIs that expect functional interfaces

Although nowadays lambdas are generally preferred for functional interfaces.
# Important things to remember
- An anonymous class is a class without an explicit name.
- You define and instantiate it in one expression.    
- It can implement an interface or extend a class.    
- It can override methods and define additional methods and fields.    
- It can access effectively final local variables from its enclosing scope.    
- It has its own `this` reference.    
- For functional interfaces, lambda expressions are usually a simpler alternative.    

One recommendation: Since you're learning Java for backend development, I'd focus more on understanding lambdas and functional interfaces after learning anonymous classes. You'll encounter them frequently in Java APIs, particularly when working with collections, streams, asynchronous operations, and Spring.