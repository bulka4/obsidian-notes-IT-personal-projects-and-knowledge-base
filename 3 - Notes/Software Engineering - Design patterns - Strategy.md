Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Strategy pattern is a pattern where, instead of using multiple algorithms inside one function with the `if/else` statement, we provide as an argument what algorithm to use.
# Example
For example, instead of creating a function like this:
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

we can simplify it such that we specify which object to use for calculations as an argument:
```python
class Order:
    def __init__(self, discount_strategy: DiscountStrategy):
        self.discount_strategy = discount_strategy

    def calculate_price(self, price):
        return self.discount_strategy.apply(price)
```

define the interface, such that in the `Order` class we will be using only implementations of this interface:
```python
from abc import ABC, abstractmethod

class DiscountStrategy(ABC):
    @abstractmethod
    def apply(self, price):
        pass
```

and define different implementations that we will be able to use in the `Order` class:
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
