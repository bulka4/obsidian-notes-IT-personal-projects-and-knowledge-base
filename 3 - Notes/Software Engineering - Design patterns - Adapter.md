Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Adapter allows a class with one interface ([[Software Engineering - Architecture concepts - Interface|link]]) to be used where a different interface is expected.
# Example
For example when we have an interface like this:
```python
from abc import ABC, abstractmethod

class PaymentGateway(ABC):
    @abstractmethod
    def pay(self, amount):
        pass
```

and we use the `pay` method in our code:
```python
def checkout(gateway):
    gateway.pay(100)
```

and we want to use a third-party service which provides:
```python
class StripeAPI:
    def charge_card(self, value):
        print(f"Charged {value}")
```

then, we can't use it directly because it provides the method called `charge_card` instead of `pay`, so our current code would not work:
```python
gateway = StripeAPI()
gateway.pay(100) # pay method doesn't exist
```

We would need to change `gateway.pay()` into `gateway.charge_card()` everywhere.

Instead, it is easier to use an adapter:
```python
# Adapter class StripeAdapter
class StripeAdapter:
    def __init__(self, stripe):
        self.stripe = stripe

    def pay(self, amount):
        self.stripe.charge_card(amount)
        
# Use the adapter to create the gateway object
stripe = StripeAPI()
gateway = StripeAdapter(stripe)

gateway.pay(100) # pay method works
```
