Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Strategy pattern allows us to define multiple algorithms/behaviors and choose between them at runtime without changing the code that uses them.

It works like this:
- We create a function
- We provide as an argument which object to use inside
- The object that we use needs to an implementation of a specific interface ([[Software Engineering - Architecture concepts - Interface|link]])
# Example
Suppose we have a function like this:
```python
class Order:
    def __init__(self, discount_type):
        self.discount_type = discount_type

    def calculate_price(self, price):
        if self.discount_type == "student":
            return price * 0.8
        elif self.discount_type == "vip":
            return price * 0.7
```

The `if` section can become big when we have a lot of conditions.

Instead, we can simplify it such that we specify which object to use for calculations as an argument:
```python
class Order:
    def __init__(self, discount_strategy: DiscountStrategy):
        self.discount_strategy = discount_strategy

    def calculate_price(self, price):
        return self.discount_strategy.apply(price)
```

Define the interface, such that in the `Order` class we will be using only implementations of this interface:
```python
from abc import ABC, abstractmethod

class DiscountStrategy(ABC):
    @abstractmethod
    def apply(self, price):
        pass
```

And define different implementation that we will be able to use in the `Order` class:
```python
class StudentDiscount(DiscountStrategy):
    def apply(self, price):
        return price * 0.8

class VipDiscount(DiscountStrategy):
    def apply(self, price):
        return price * 0.7
```

Then we can choose which implementation to use:
```python
order = Order(StudentDiscount()) # Or use VipDiscount or any other implementation
order.calculate_price(100)
```
