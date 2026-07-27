Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Observer pattern is used when one class needs to call a lot of methods of other classes. If we use multiple classes inside another class, then that class becomes dependent on those other classes.

To avoid this, we can use the observer pattern where one object (called subject) automatically notifies multiple other objects (called observers) to perform different actions.

Then, when the subject needs to perform some actions, it only needs to notify observers to do this and the subject doesn't need to know how exactly those actions will look like.
# Example
Suppose we have an e-commerce system where when order status changes (e.g. it is getting shipped), then multiple other actions need to happen:
- send an email
- update inventory

Without observer, the `Order` class would need to use a lot of functions:
```python
send_email()
update_inventory()
```

so it would become dependent on those functions.

Instead, we can create the `Order` class like this:
```python
class Order:
    def __init__(self):
        self.observers = []

    def subscribe(self, observer):
        self.observers.append(observer)

    def notify(self, event):
        for observer in self.observers:
            observer.update(event)

    def ship(self):
        self.notify("Order shipped")
```

So it will just notify all the observers when a product is shipped and they will perform all the necessary actions. The `Order` class doesn't know what actions specifically.

We define an interface for observers:
```python
from abc import ABC, abstractmethod

class Observer(ABC):
    @abstractmethod
    def update(self, event):
        pass
```

and multiple implementations:
```python
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