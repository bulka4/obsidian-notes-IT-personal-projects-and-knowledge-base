Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The factory design pattern ([[Software Engineering - Object-oriented design - Design patterns|link]]) is used to abstract away a process of creating an object.

For example, instead of writing:
```python
if payment_type == "stripe":
	payment = StripePayment()
elif payment_type == "paypal":
	payment = PaypalPayment()
```

We can define a factory:
```python
class PaymentFactory:
    @staticmethod
    def create(payment_type):
        if payment_type == "stripe":
            return StripePayment()
        elif payment_type == "paypal":
            return PaypalPayment()
```

and use it for creating objects:
```python
payment = PaymentFactory.create("stripe")
```