Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
An abstract class is a class that cannot be instantiated directly. Within an abstract class we can define:
- normal methods that are inherited by child classes
- abstract classes that are not defined in the abstract class and every child class must implement them (override)

Example:
```java
public abstract class Animal {
	// this method must be override by every child class
    public abstract void makeSound();

    public void sleep() {
        System.out.println("Sleeping...");
    }
}
```

Notice two things:
- `makeSound()` is an abstract method. It has no implementation.
- `sleep()` is a regular method with an implementation.

Now we can create child classes:
```java
public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}
```

```java
public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}
```

We cannot do:
```java
Animal animal = new Animal(); // Compilation error
```

But we can do:
```java
Animal dog = new Dog();
Animal cat = new Cat();

dog.makeSound(); // Woof!
cat.makeSound(); // Meow!
```

The abstract class defines what functionality subclasses must provide, without specifying exactly how they implement it.
