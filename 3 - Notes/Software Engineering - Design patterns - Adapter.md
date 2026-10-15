Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Adapter is a technique where we convert a class which is an invalid implementation of an interface ([[Software Engineering - Object-oriented design - Interfaces|link]]), into a new class which is valid.

A class might be invalid for example because its methods are called differently or argument type are different.
# Example
For example, when our interface specifies that each implementation should have the `pay` method:
```python
from abc import ABC, abstractmethod

class PaymentGateway(ABC):
    @abstractmethod
    def pay(self, amount):
        pass
```

and we have a class with a method called differently:
```python
class StripeAPI:
    def charge_card(self, value):
        print(f"Charged {value}")
```

We can create a new class that will convert the `StripeAPI` class into a valid implementation of the `PaymentGateway` interface with the `pay` method:
```python
# Adapter class StripeAdapter
class StripeAdapter:
    def __init__(self, stripe):
        self.stripe = stripe

    def pay(self, amount):
        self.stripe.charge_card(amount)
```
