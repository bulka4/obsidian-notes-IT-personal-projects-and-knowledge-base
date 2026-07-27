Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Object-oriented design (OOD) is the process of designing software by modeling it as a collection of objects that represent data and behavior.

An object combines:
- State → data (attributes)
- Behavior → actions (methods)
# Example
```python
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
- **Polymorphism** → the same interface ([[Software Engineering - Architecture concepts - Interface|link]]) can have different implementations depending on the object that uses it. In simpler words, we can specify in one class which methods exist and define their logic in other classes.
## Example - Polymorphism
```python
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
# Related topics
1. [[Software Engineering - Object-oriented design - SOLID]]
2. [[Software Engineering - Object-oriented design - Composition vs inheritance]]
3. [[Software Engineering - Object-oriented design - Interfaces]]
4. [[Software Engineering - Object-oriented design - Protocols]]
5. [[Software Engineering - Object-oriented design - Design patterns]]