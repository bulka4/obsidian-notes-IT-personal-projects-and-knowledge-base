Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
- An interface defines a contract that implementing classes must follow.
- We don't define a logic of methods of an interface
- When a class implements an interface, it must define a logic for all methods of this interface
- An object of a class is also an object of the interface class that this class implements
	- So for example, if `CreditCardProcessor` implements `PaymentProcessor`, then object of the `CreditCardProcessor` class is also an object of the `PaymentProcessor` class
	- Thanks to this, we can for example define in a function that a specific argument needs to be an object of an interface class, so it can be any class that implements this interface, so it posses specific methods defined in this interface but it doesn't matter how those methods are implemented
# Example
```java
public interface PaymentProcessor {
    void processPayment(double amount);
}
```

Different classes can implement this interface:
```java
public class CreditCardProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment");
    }
}
```

```java
public class PayPalProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing PayPal payment");
    }
}
```

Now imagine you have a service that processes payments:
```java
public class PaymentService {
	// As the "processor" argument we can use an object of any class
	// that implements the PaymentProcessor interface
    public void pay(PaymentProcessor processor, double amount) {
        processor.processPayment(amount);
    }
}
```

You can pass either implementation:
```java
PaymentService service = new PaymentService();

service.pay(new CreditCardProcessor(), 100);
service.pay(new PayPalProcessor(), 100);
```

The `PaymentService` doesn't need to know how credit card or PayPal payments work. It only needs to know that the supplied object implements `PaymentProcessor`.
# Default methods
A default method is a method in an interface that has an implementation (method body).

Normally, interfaces define methods that implementing classes must implement. Default methods  don't have to be implemented but can be overridden.
```java
interface Vehicle {
    void start();

    default void honk() {
        System.out.println("Beep!");
    }
}
```
# Related topics
1. [[Java - Functional interface]]
2. [[Java - Marker interface]]
3. [[Java - Sealed interfaces]]