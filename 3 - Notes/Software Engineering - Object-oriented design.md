Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Object-oriented design (OOD)** is the process of designing software by modeling it as a collection of **objects** that represent data and behavior.

An **object** combines:
- **State** → data (attributes)
- **Behavior** → actions (methods)
# Example
```
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        self.balance -= amount
```

Here:
- `balance` → state
- `withdraw()` → behavior
# Key concepts
- **Encapsulation** → keep data and related operations together; control access to internal state.
- **Abstraction** → expose only necessary details, hide implementation.
- **Inheritance** → create new classes based on existing ones.
- **Polymorphism** → different objects can respond to the same interface differently.
## Example
```
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def area(self):
        return 3.14 * r * r

class Square(Shape):
    def area(self):
        return side * side
```

Both `Circle` and `Square` provide `area()`, but implement it differently.
# Good OOD usually focuses on
- Clear responsibilities (each class does one main thing)
- Low coupling (classes depend less on each other)
- High cohesion (related functionality stays together)
- Reusable and testable components
# Common design principles
- **SOLID principles**
- **Design patterns** (Factory, Strategy, Observer, etc.)