Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
In Java, there are no standalone functions. Every function must be a method that belongs to a class, interface, enum or record.

We can't just define a function like in Python:
```python
def greet():
    print("Hello")
```

It needs to be for example in a class:
```java
public class Main {

    public static void greet() {
        System.out.println("Hello");
    }

    public static void main(String[] args) {
        greet();
    }
}
```
# Syntax
The general syntax for defining a method in Java is:
```java
[access_modifier] [other_modifiers] return_type methodName(parameters) {
    // method body
}
```
## Modifiers (access and other)
[[Java - Modifiers]]
## Return type
Specifies what type of value the method returns. `void` means that it returns nothing.
## Variable number of parameters (varargs)
Allow to provide different number of parameters each time we call the method:
```java
public int sum(int... numbers) {
    int result = 0;

    for (int number : numbers) {
        result += number;
    }

    return result;
}
```
## Throws clause
A method can declare which exceptions it might throw.
```java
public void readFile() throws IOException, SQLException {
    // Read file
}
```
## Parameters
Parameters have this structure:
```java
methodName([annotations] Type parameterName)
```

for example:
```java
public void greet(@SomeAnnotation String name)
```
- `@SomeAnnotation` — annotation that provides instructions for how to prepare or validate the `name` parameter. 
	- It can run a defined method to prepare the parameter and then the `greet` method will be executed with this parameter.
	- Or it can run a defined method to validate the parameter and throw an exception if the parameter is incorrect
- `String` — the parameter's type.    
- `name` — the parameter's name.
# Related topics
1. [[Java - Generic methods]]