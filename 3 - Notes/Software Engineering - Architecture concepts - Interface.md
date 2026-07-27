Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
An interface specifies what operations are available, but not how they are implemented. 

It is a contract that defines how one part of a system can communicate with another part.
# Interface implementation
Interface implementation is a specific implementation of operations defined by an interface. 
# Example
For example, it can be a class that specifies what methods are available but not how their logic is implemented:
```python
class PaymentGateway:
    def pay(self, amount):
        pass
```

Then, we can create another class (implementation of an interface) that defines a logic for those methods:
```python
class PaypalPayment(PaymentGateway):
    def pay(self, amount):
        # call PayPal API
        ...
        pass
```
# Using an interface as a dependency
We can use an interface as a dependency ([[Software Engineering - Dependency management|link]]) for our application and use any implementation we want, for example by providing it as an argument.

For example, we can have a function where we require that argument is an object of some class (that class is an interface, a dependency):
```python
class OrderService:
    def __init__(self, payment_gateway: PaymentGateway):
        self.payment_gateway = payment_gateway
```
so this way we define that we need to use a class that contains the `save` method.

And we provide a specific implementation of that interface (`PaypalPayment`) as an argument:
```python
# Use PaypalPayment or any other implementation
order_service = OrderService(payment_gateway=PaypalPayment())
```
# Other examples
An interface doesn't have to be a class:
## 1. Component interface (architecture)
A component exposes operations to other components:
```
Order Component

Public interface:
    create_order()
    cancel_order()
    get_order()
```

The internal classes are hidden.
## 2. API interface
A REST API is also an interface:
```
POST /orders
GET /orders/{id}
DELETE /orders/{id}
```

The interface is the set of available endpoints and their contracts.
## 3. Event interface
Components can communicate through events:
```json
{
  "event": "OrderCreated",
  "orderId": 123
}
```

The event format is the interface.
# Dependency injection
Providing a specific interface implementation to an application is an example of a dependency injection ([[Software Engineering - Dependency injection|link]]).