Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Observer pattern is a pattern where one object (called a subject), instead of performing many different operations on its own, it notifies other objects (called observers) to perform all the necessary actions for it. 

The subject doesn't need to know what actions are performed exactly. Thanks to this, it becomes independent on those actions logic. We can later change observers' logic or add new observers without changing the subject.
# Example
For example, in an e-commerce app, when an order is shipped, we might need to perform multiple actions, like:
- send an email
- update inventory

Instead of performing all those actions by one object:
```python
class Order:
	def send_email(...)
		...
		
	def update_inventory(...)
		...
		
	def ship(...)
		self.send_email()
		self.update_inventory()
```

the `Order` object might notify all the observers to perform all the necessary actions:
```python
class Order:
    def __init__(self):
        self.observers = []

    def subscribe(self, observer: Observer):
        self.observers.append(observer)

    def notify(self, event):
        for observer in self.observers:
            observer.update(event)

    def ship(self):
        self.notify("Order shipped")
```

and observers actions logic is implemented separately, outside of the `Order` class:
```python
from abc import ABC, abstractmethod

class Observer(ABC):
    @abstractmethod
    def update(self, event):
        pass
        
class EmailNotifier(Observer):
    def update(self, event):
        print(f"Sending email: {event}")

class InventoryService(Observer):
    def update(self, event):
        print(f"Updating inventory because of the event: {event}")
```

and we use it like this:
```python
order = Order()

order.subscribe(EmailNotifier())
order.subscribe(InventoryService())

order.ship()
```

Output:
```
Sending email: Order shipped
Updating inventory because of the event: Order shipped
```

So the `Order` class doesn't know about what exactly happens when a product is shipped. It only notifies observers and observers handles all the job. 

We can later change what happens when an order is shipped (change observer's logic) without changing the `Order` class and how it is used.