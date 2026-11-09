Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Access modifiers are useful because they allow you to control which parts of your application can access or modify other parts.

This is one of the foundations of object-oriented programming, particularly a concept called encapsulation.
# Preventing unwanted modifications
Imagine you have a `BankAccount` class:
```
public class BankAccount {
    public double balance = 1000;
}
```

Anyone who has access to an instance of this class can modify its balance:
```
BankAccount account = new BankAccount();

account.balance = -500000;
```

This is problematic because you probably don't want arbitrary parts of your application to change an account's balance.

Instead, you can make the variable private:
```
public class BankAccount {
    private double balance = 1000;
}
```

Now this won't work:
```
account.balance = -500000;
```

The compiler rejects it.

You've restricted direct access to the internal state of your object.
# Controlling how data is modified
Making a variable private doesn't mean nobody can modify it.

You can expose methods (getters and setters ([[Java - Getters and setters|link]])) that allow controlled modifications:
```
public class BankAccount {
    private double balance = 1000;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

Now other parts of your application can:
```
account.deposit(500);

System.out.println(account.getBalance());
```

But they cannot directly assign an arbitrary value to `balance`.

This gives you several benefits:
- You can validate input.    
- You can enforce business rules.    
- You can prevent invalid states.    
- You can change the internal implementation without changing how other classes interact with it.    

This is encapsulation in practice.
# Hiding implementation details
Imagine you're developing a backend application with hundreds of classes.

One class might have several internal helper methods:
```
public class UserService {

    public void createUser(String username) {
        validateUsername(username);
        saveUser(username);
    }

    private void validateUsername(String username) {
        // Internal validation logic
    }

    private void saveUser(String username) {
        // Database operation
    }
}
```

Other classes only need to know about `createUser()`.

They don't need to know how validation and database operations are implemented.

By making helper methods private, you communicate that they are implementation details, not part of the class's public interface.

This makes your codebase easier to maintain.
# Questions
- what is encapsulation?