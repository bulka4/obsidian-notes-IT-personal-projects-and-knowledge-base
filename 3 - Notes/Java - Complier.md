Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
The compiler in Java in catch errors before running the program which is very important when running a lot of code.

It also makes code easier to maintain and refactor because, if for example 50 other places in your application call this method using an integer, the compiler can identify those places as compilation errors.
# Catching errors before execution
The compiler in Java in catch errors before running the program which is very important when running a lot of code.
## What errors the compiler can check
### Variable declaration and scope errors
The compiler checks whether variables exist and are accessible where you're trying to use them.
```java
public void calculate() {
    int result = 10;
}

public void printResult() {
    System.out.println(result);
}
```

This won't compile because `result` is local to the `calculate()` method. It isn't accessible inside `printResult()`.
### Others
- whether we declare and handle exceptions properly ([[Java - Exception handling|link]])
- syntax errors
	- e.g. missing semicolon - `int age = 25`
- variable type errors
	- e.g. `int age = "25";`
- incorrect method calls
	- passing incorrect arguments
- Incorrect return statements
	- returning a value of a different type then declared in the method:
	  ```java
		public int getAge() {
			return "25";
		}
	  ```
### Access modifier violations
Java has access modifiers such as `public`, `private` and `protected` ([[Java - Modifiers|link]]).

The compiler checks whether you're allowed to access particular classes, methods and variables.

For example:
```java
class User {
    private String password = "secret";
}

public class Main {
    public static void main(String[] args) {
        User user = new User();
        System.out.println(user.password);
    }
}
```

This won't compile because `password` is private and cannot be accessed directly from `Main`.
### Interface and abstract class implementation errors
Suppose you have an interface:
```java
interface Payment {
    void processPayment();
}
```

And a class implementing it:
```java
class CreditCardPayment implements Payment {
}
```

This won't compile because `CreditCardPayment` hasn't implemented the required `processPayment()` method.

The compiler enforces the contract defined by the interface.
### Checked exception handling errors
Java has checked exceptions, which must be handled or declared.

For example:
```java
import java.io.FileReader;

public class Main {
    public static void main(String[] args) {
        FileReader reader = new FileReader("test.txt");
    }
}
```

This won't compile because `FileReader` can throw an `IOException`, which must be handled or declared.

You could fix it using `try-catch`:
```java
try {
    FileReader reader = new FileReader("test.txt");
} catch (IOException e) {
    System.out.println("Could not open file");
}
```
# Making code easier to maintain and refactor
For example, when we change a method:
```java
// Old
public String getUserName(int userId) {
    // ...
}

//New
public String getUserName(String userId) {
    // ...
}
```

If 50 other places in your application call this method using an integer, the compiler can identify those places as compilation errors.