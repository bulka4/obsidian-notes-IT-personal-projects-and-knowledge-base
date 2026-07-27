Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Modularity is the principle of designing software as a collection of separate, independent components (modules) that have clear responsibilities and controlled interactions.

The main goal:
> Divide a complex system into smaller parts that can be developed, tested, changed, and understood independently.
# 1. What is a module?
A module is a self-contained unit of functionality (usually a collection of scripts to use in other scripts).

Example: A webshop:
```
E-commerce application

├── User module
│   ├── Authentication
│   └── User profile
│
├── Order module
│   ├── Cart
│   └── Checkout
│
├── Payment module
│   ├── Stripe integration
│   └── PayPal integration
│
└── Notification module
    ├── Email
    └── SMS
```

Each module owns a specific area of functionality.
# Good modularity properties
- High cohesion - A module should contain things that belong together - no unnecessary, unrelated things
- Low coupling - Modules should depend on each other as little as possible.
## Modules communicate through interfaces
Use interfaces ([[Software Engineering - Architecture concepts - Interface|link]]), for example:

Payment module:
```python
from abc import ABC, abstractmethod

class PaymentService(ABC):
    @abstractmethod
    def pay(self, amount):
        pass
```

Implementation:
```python
class StripePayment(PaymentService):
    def pay(self, amount):
        print(f"Paid {amount} using Stripe")
```

Order module:
```python
class OrderService:
    def __init__(self, payment_service):
        self.payment_service = payment_service

    def checkout(self):
        self.payment_service.pay(100)
```

The Order module does not know about Stripe.
# Benefits of modularity
- Easier maintenance - We can update only a module without updating the app that uses it
- Easier testing - We can test each module independently
- Parallel development - Teams can work independently on different modules
- Reusability - A module can be reused across different applications
- 