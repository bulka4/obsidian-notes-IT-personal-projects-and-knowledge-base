Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Design patterns are reusable solutions to common software design problems.

They are not ready-made code, but rather **templates or best practices** for structuring code.
# Examples
## Creational patterns (object creation)
- **Factory** → encapsulates object creation.
- **Singleton** → ensures only one instance exists.
## Structural patterns (object relationships)
- **Adapter** → makes incompatible interfaces work together.
- **Decorator** → adds functionality without modifying a class.
- **Facade** → provides a simpler interface to a complex system.
## Behavioral patterns (object interaction)
- **Strategy** → encapsulates interchangeable algorithms.
- **Observer** → notifies multiple objects about changes.
- **Command** → encapsulates a request as an object.
# Example: Strategy pattern
```python
class PaymentStrategy:
    def pay(self):
        pass

class CardPayment(PaymentStrategy):
    def pay(self):
        print("Card")

class PaypalPayment(PaymentStrategy):
    def pay(self):
        print("PayPal")
```

Usage:
```python
class Checkout:
    def __init__(self, strategy):
        self.strategy = strategy

    def pay(self):
        self.strategy.pay()
```

Now you can easily swap payment methods.

Benefits of design patterns:
- Use proven solutions
- Improve maintainability and flexibility
- Provide a common vocabulary among developers